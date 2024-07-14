[TOC]


The share level of Kyuubi engines describes the relationship between sessions and engines.
It determines whether a new session can share an existing backend engine with other sessions or not.
The sessions are also known as JDBC/ODBC/Thrift connections from clients that end-users create, and the engines are standalone applications with the full capabilities of Spark SQL, Flink SQL(under dev), running on single-node machines or clusters.

The share level of Kyuubi engines works the same whether in HA or single node mode.
In other words, an engine is cluster widely shared by all Kyuubi server peers if could.

## Why do we need this feature?

Apache Spark is a unified engine for large-scale data analytics.
Using Spark to process data is like driving an all-wheel-drive hefty horsepower supercar.
However,

- Cars have their limit of 0-60 times.
  In a similar way, all Spark applications also have to warm up before go full speed.
- Cars have a constant number of seats and are not allowed to be overloaded.
  Due to the master-slave architecture of Spark and the resource configured ahead, the overall workload of a single application is predictable.
- Cars have various shapes to meet our needs.

With this feature, Kyuubi give you a more flexible way to handle different big data workloads.

## The current supported share levels

The current supported share levels are,

|  Share Level   |            Syntax            |           Scenario           |               Isolation Degree               |     Shareability      |
|----------------|------------------------------|------------------------------|----------------------------------------------|-----------------------|
| **CONNECTION** | One engine per session       | Large-scale ETL </br> Ad hoc | High                                         | Low                   |
| **USER**       | One engine per user          | Ad hoc </br> Small-scale ETL | Medium                                       | Medium                |
| **GROUP**      | One engine per primary group | Ad hoc </br> Small-scale ETL | Low                                          | High                  |
| **SERVER**     | One engine per cluster       | Admin                        | Highest If Secured </br> Lowest If Unsecured | Admin ONLY If Secured |

- Better isolation degree of engines gives us better stability of an engine and the query executions running on it.
- Better shareability of engines means we are more likely to reuse an engine which is already in full speed.

### CONNECTION

![](https://cdn.north.devlive.org/images/2024/07/14/17209696833744.jpg)

Each session with CONNECTION share level has a standalone engine for itself which is unreachable for anyone else.
Within the session, a user or client can send multiple operation request, including metadata calls or queries, to the corresponding engine.

Although it is still an interactive form, this model does allow for more practical batch processing jobs as well.

When closing session, the corresponding engine will be shutdown at the same time.

### USER(Default)

![](https://cdn.north.devlive.org/images/2024/07/14/17209697585162.jpg)

All sessions with USER share level use the same engine if and only if the session user is the same.

Those sessions share the same engine with objects belong to the one and only `SparkContext` instance, including `Classes/Classloaders`, `SparkConf`, `Driver`/`Executor`s, `Hive Metastore Client`, etc.
But each session can still have its own `SparkSession` instance, which contains separate session state, including temporary views, SQL config, UDFs etc.
Setting `kyuubi.engine.single.spark.session` to true will make `SparkSession` instance a singleton and share across sessions.

When closing session, the corresponding engine will not be shutdown.
When all sessions are closed, the corresponding engine still has a time-to-live lifespan.
This TTL allows new sessions to be established quickly without waiting for the engine to start.

### GROUP

![](https://cdn.north.devlive.org/images/2024/07/14/17209697938664.jpg)

An engine will be shared by all sessions created by all users belong to the same primary group name.
The engine will be launched by the group name as the effective username, so here the group name is kind of special user who is able to visit the compute resources/data of a team.
It follows the [Hadoop GroupsMapping](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/GroupsMapping.html) to map user to a primary group. If the primary group is not found, it falls back to the USER level.

The mechanisms of `SparkContext`, `SparkSession` and TTL works similarly to USER share level.

**Tips for authorization in GROUP share level**:

The session user and the primary group name(as sparkUser/execute user) will be both accessible at engine-side.
By default, the sparkUser will be used to check the YARN/HDFS ACLs.
If you want fine-grained access control for session user, you need to get it from `SparkContext.getLocalProperty("kyuubi.session.user")` and send it to security service, like Apache Ranger.

### SERVER

![](https://cdn.north.devlive.org/images/2024/07/14/17209698223626.jpg)

Literally, this model is similar to Spark Thrift Server with High availability.

### Subdomain

For USER, GROUP, or SERVER share levels, you can further use `kyuubi.engine.share.level.subdomain` to isolate the engine.
That is, you can also create multiple engines for a single user, group or server(cluster).
For example, in USER share level, you can use `kyuubi.engine.share.level.subdomain=sd1` and `kyuubi.engine.share.level.subdomain=sd2` to create two standalone engines for user `Tom`.

The `kyuubi.engine.share.level.subdomain` shall be configured in the JDBC connection URL to tell the Kyuubi server which engine you want to use.

### Hybrid

All supported share levels can be used together in a single Kyuubi server or cluster.

## Related Configurations

- kyuubi.engine.share.level(kyuubi.session.engine.share.level)
    - Default: USER
    - Candidates: USER, CONNECTION, GROUP, SERVER
    - Meaning: The base level for how an engine is created, cached and shared to sessions.
    - Usage: It can be set both in the server configuration file and also connection URL. The latter has higher priority.
- kyuubi.session.engine.idle.timeout
    - Default: PT30M (30 min)
    - Candidates: a proper timeout
    - Meaning: Time to live since engine becomes idle
    - Usage: It can be set both in the server configuration file and also connection URL. The latter has higher priority.
- kyuubi.engine.share.level.subdomain(kyuubi.engine.share.level.sub.domain)
    - Default: <none>
    - Candidates: a valid zookeeper a child node
    - Meaning: Add a subdomain under the base level to make further isolation for engines
    - Usage: It can be set both in the server configuration file and also connection URL. The latter has higher priority.

## Conclusion

With this feature, end-users are able to leverage engines in different ways to handle their different workloads, such as large-scale ETL jobs and interactive ad hoc queries.

