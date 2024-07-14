[TOC]

As an enterprise-class ad-hoc SQL query service built on top of [Apache Spark](https://spark.apache.org/), Kyuubi takes high availability (HA) as a major characteristic, aiming to ensure an agreed level of service availability, such as a higher than normal period of uptime.

Running Kyuubi in HA mode is to use groups of computers or containers that support SQL query service on Kyuubi that can be reliably utilized with a minimum amount of down-time. Kyuubi operates by using [Apache ZooKeeper](https://zookeeper.apache.org/) to harness redundant service instances in groups that provide continuous service when one or more components fail.

Without HA, if a server crashes, Kyuubi will be unavailable until the crashed server is fixed. With HA, this situation will be remedied by hardware/software faults auto-detecting, and immediately another Kyuubi service instance will be ready to serve without requiring human intervention.

## HA Architecture

Currently, Kyuubi supports load balancing to make the whole system highly available.

Load balancing aims to optimize all Kyuubi service unit's usage, maximize throughput, minimize response time, and avoid overload of a single unit.
Using multiple Kyuubi service units with load balancing instead of a single unit may increase reliability and availability through redundancy.

![](https://cdn.north.devlive.org/images/2024/07/14/17209692453874.jpg)

### Key Benefits

- High concurrency
    - By adding or removing Kyuubi server instances can easily scale up or down to meet the need of client requests.
- Upgrade smoothly
    - Kyuubi server supports stopping gracefully. We could delete a `k.i.` but not stop it immediately.
      In this case, the `k.i.` will not take any new connection request but only operation requests from existing connections.
      After all connection are released, it stops then.
    - The dependencies of Kyuubi engines are free to change, such as bump up versions, modify configurations, add external jars, relocate to another engine home. Everything will be reloaded during start and stop.

## System-side Deployment

When applying HA to Kyuubi deployment, we need to be aware of the below two thing basically,

- `kyuubi.ha.addresses` - the external zookeeper cluster address for deploy a `k.i.`
- `kyuubi.ha.namespace` - the root directory, a.k.a. the ServerSpace for deploy a `k.i.`

For more configurations, please see the HA section of [Introduction to the Kyuubi Configurations System](./settings.html#ha)

### Pseudo mode

When `kyuubi.ha.addresses` is not configured, a `k.i.` will start an embedded zookeeper service and expose the address of itself there.
In this pseduo mode, the `k.i.` can be connected by clients through both raw ip address and zk quorum + namespace.
But it doesn't have any availability to being highly available.

### Production mode

For production deployment purpose, an external zookeeper cluster is required for `kyuubi.ha.addresses`.
In this mode, multiple `k.i.`s can be registered to the same ServerSpace configured by `kyuubi.ha.namespace` and serve together.

## Client-side Usage

With [Kyuubi Hive JDBC Driver](https://mvnrepository.com/artifact/org.apache.kyuubi/kyuubi-hive-jdbc) or vanilla Hive JDBC Driver, a client can specify service discovery mode in JDBC connection string, i.e. `serviceDiscoveryMode=zooKeeper;` and set `zooKeeperNamespace=kyuubi;`, then it can randomly pick one of the Kyuubi service uris from the specified ZooKeeper addresses in the `/kyuubi` path.

For example,

```shell
bin/beeline -u 'jdbc:hive2://10.242.189.214:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=kyuubi' -n kentyao
```

## How to Hot Upgrade Kyuubi Server

Kyuubi supports hot upgrade one of server in a HA cluster which is transparent to users.

- If you have specified a custom port for Kyuubi server

  For example, the Kyuubi server started at host `kyuubi.host` with port `10009`, you can run the following cmd using `bin/kyuubi-ctl`:

  ```shell
  ./bin/kyuubi-ctl delete server --host "kyuubi.host" --port "10009"
  ```

  Kyuubi server will stop until all session closed, and then you can start a new Kyuubi server.

- If you use a random port for Kyuubi server

  You can just start the new Kyuubi Server, and then run cmd using `bin/kyuubi-ctl`:

  ```shell
  ./bin/kyuubi-ctl delete server --host "kyuubi.host" --port "${PORT_FPR_OLD_KYUUBI_SERVER}"
  ```

  The `${PORT_FPR_OLD_KYUUBI_SERVER}` can be found by:

  ```shell
  grep "server.KyuubiThriftBinaryFrontendService: Starting and exposing JDBC connection at" logs/kyuubi-*.out
  ```

  Note that, you do not need to care when the old Kyuubi server actually stopped since the new coming session are routed to the new Kyuubi server and others.


