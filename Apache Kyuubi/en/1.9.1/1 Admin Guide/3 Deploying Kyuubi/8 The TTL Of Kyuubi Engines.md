[TOC]


For a multi-tenant cluster, its overall resource utilization is a KPI that measures how effectively its resource is utilized against its availability or capacity.
To better improve the overall resource utilization of the cluster,
- At cluster layer, we leverage the capabilities, such as [Capacity Scheduler](https://hadoop.apache.org/docs/stable/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html), of resource scheduling management services, such as YARN and K8s.
- At application layer, we'd be better to acquire and release resources according to the real workloads.

## The Big Contributors Of Resource Waste

- The time to wait for the resource to be allocated, such as the scheduling delay, the start/stop cost.
    - A longer time-to-live(TTL) for allocated resources can significantly reduce such time costs within an application.
- The time being idle of the resource.
    - A shorter time to live for allocated resources can make all resources in rapid turnarounds across applications.

## TTL Types In Kyuubi Engines

![](https://cdn.north.devlive.org/images/2024/07/14/17209699291317.jpg)

- Engine TTL
    - The TTL of engines describes how long an engine will be cached after all sessions are disconnected.
- Executor TTL
    - The TTL of the executor describes how long an executor will be cached when no tasks come.

## Configurations

### Engine TTL

|                     Key                      |                                    Default                                     |                                                                                                    Meaning                                                                                                    |                  Type                   |                Since                 |
|----------------------------------------------|--------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------|--------------------------------------|
| kyuubi\.session\.engine<br>\.check\.interval | <div style='width: 65pt;word-wrap: break-word;white-space: normal'>PT5M</div>  | <div style='width: 170pt;word-wrap: break-word;white-space: normal'>The check interval for engine timeout</div>                                                                                               | <div style='width: 30pt'>duration</div> | <div style='width: 20pt'>1.0.0</div> |
| kyuubi\.session\.engine<br>\.idle\.timeout   | <div style='width: 65pt;word-wrap: break-word;white-space: normal'>PT30M</div> | <div style='width: 170pt;word-wrap: break-word;white-space: normal'>engine timeout, the engine will self-terminate when it's not accessed for this duration. 0 or negative means not to self-terminate.</div> | <div style='width: 30pt'>duration</div> | <div style='width: 20pt'>1.0.0</div> |

The above two configurations can be used together to set the TTL of engines.
These configurations are user-facing and able to use in JDBC urls.
Note that, for [connection]($The-Share-Level-Of-Kyuubi-Engines#connection) share level engines that will be terminated at once when the connection is disconnected, these configurations not necessarily work in this case.

### Executor TTL

Executor TTL is part of functionality of Apache Spark's [Dynamic Resource Allocation]($How-To-Use-Spark-Dynamic-Resource-Allocation-DRA-In-Kyuubi).

