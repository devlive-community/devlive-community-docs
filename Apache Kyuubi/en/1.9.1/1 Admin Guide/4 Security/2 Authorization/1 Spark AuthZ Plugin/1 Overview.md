[TOC]

Security is one of the fundamental features for enterprise adoption with Kyuubi. When deploying Kyuubi against secured clusters, storage-based authorization is enabled by default, which only provides file-level coarse-grained authorization mode. When row/column-level fine-grained access control is required, we can enhance the data access model with the Kyuubi Spark AuthZ plugin.

Authorization in Kyuubi
-------------------------------------------------------------------------------------------------------------------------------------------------------------

### Storage-based Authorization

As Kyuubi supports multi tenancy, a tenant can only visit authorized resources, including computing resources, data, etc. Most file systems, such as HDFS, support ACL management based on files and directories.

A so called Storage-based authorization mode is supported by Kyuubi by default. In this model, all objects, such as databases, tables, partitions, in meta layer are mapping to folders or files in the storage layer, as well as their permissions.

Storage-based authorization offers users with database, table and partition-level coarse-gained access control.

### SQL-standard authorization with Ranger

A SQL-standard authorization usually offers a row/colum-level fine-grained access control to meet the real-world data security need.

[Apache Ranger](https://ranger.apache.org/) is a framework to enable, monitor and manage comprehensive data security across the Hadoop platform. This plugin enables Kyuubi with data and metadata control access ability for Spark SQL Engines, including,

*   Column-level fine-grained authorization
*   Row-level fine-grained authorization, a.k.a. Row-level filtering
*   Data masking

The Plugin Itself
-------------------------------------------------------------------------------------------------------------------------------------------------

Kyuubi Spark Authz Plugin itself provides general purpose for ACL management for data & metadata while using Spark SQL. It is not necessary to deploy it with the Kyuubi server and engine, and can be used as an extension for any Spark SQL jobs. However, the authorization always requires a robust authentication layer and multi tenancy support, so Kyuubi is a perfect match.

### Restrict security configuration

End-users can disable the AuthZ plugin by modifying Spark’s configuration. For example:

```sql
select * from parquet.`/path/to/table`
```

```sql
set spark.sql.optimizer.excludedRules=org.apache.kyuubi.plugin.spark.authz.ranger.RuleAuthorization
```

Kyuubi provides a mechanism to ban security configurations to enhance the security of production environments

> How do we modify the Spark engine configurations please refer to the documentation [Spark Configurations]($Configurations#spark-configurations)

#### Restrict session level config

You can specify config kyuubi.session.conf.ignore.list values and config kyuubi.session.conf.restrict.list values to disable changing session+ level configuration on the server side. For example:

```sql
kyuubi.session.conf.ignore.list    spark.driver.memory,spark.sql.optimizer.excludedRules
```

```sql
kyuubi.session.conf.restrict.list    spark.driver.memory,spark.sql.optimizer.excludedRules
```

#### Restrict operation level config

You can specify config spark.kyuubi.conf.restricted.list values to disable changing operation level configuration on the engine side, this means that the config key in the restricted list cannot set dynamic configuration via SET syntax. For examples:

```sql
spark.kyuubi.conf.restricted.list  spark.sql.adaptive.enabled,spark.sql.adaptive.skewJoin.enabled
```

> 1.  Note that config spark.sql.runSQLOnFiles values and config spark.sql.extensions values are by default in the engine restriction configuration list
> 
> 2.  A set statement with key equal to spark.sql.optimizer.excludedRules and value containing org.apache.kyuubi.plugin.spark.authz.ranger.\* also does not allow modification.
