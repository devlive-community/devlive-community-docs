[TOC]

Apache Iceberg is an open table format for huge analytic datasets. Iceberg adds tables to compute engines including Spark, Trino, PrestoDB, Flink, Hive and Impala using a high-performance table format that works just like a SQL table.

> This article assumes that you have mastered the basic knowledge and operation of [Iceberg](https://iceberg.apache.org/). For the knowledge about Iceberg not mentioned in this article, you can obtain it from its [Official Documentation](https://iceberg.apache.org/docs/latest/).

By using kyuubi, we can run SQL queries towards Iceberg which is more convenient, easy to understand, and easy to expand than directly using flink to manipulate Iceberg.

Iceberg Integration
---------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi flink sql engine and Iceberg through Catalog APIs, you need to:

*   Referencing the Iceberg [dependencies](#flink-iceberg-deps)

### Dependencies

The **classpath** of kyuubi flink sql engine with Iceberg supported consists of

1.  kyuubi-flink-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of flink distribution
3.  iceberg-flink-runtime-<flink.version>-<iceberg.version>.jar (example: iceberg-flink-runtime-1.14-0.14.0.jar), which can be found in the [Maven Central](https://mvnrepository.com/artifact/org.apache.iceberg)

In order to make the Iceberg packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the Iceberg packages into `$FLINK_HOME/lib` directly
2.  Set `pipeline.jars=/path/to/iceberg-flink-runtime`

> Please mind the compatibility of different Iceberg and Flink versions, which can be confirmed on the page of [Iceberg multi engine support](https://iceberg.apache.org/multi-engine-support/).

Iceberg Operations
-------------------------------------------------------------------------------------------------------------------------------------

Taking `CREATE CATALOG` as a example,

```sql
CREATE CATALOG hive_catalog WITH (
  'type'='iceberg',
  'catalog-type'='hive',
  'uri'='thrift://localhost:9083',
  'warehouse'='hdfs://nn:8020/warehouse/path'
);
USE CATALOG hive_catalog;
```

Taking `CREATE DATABASE` as a example,

```sql
CREATE DATABASE iceberg_db;
USE iceberg_db;
```

Taking `CREATE TABLE` as a example,

```sql
CREATE TABLE `hive_catalog`.`default`.`sample` (
  id BIGINT COMMENT 'unique id',
  data STRING
);
```

Taking `Batch Read` as a example,

```sql
SET execution.runtime-mode = batch;
SELECT * FROM sample;
```

Taking `Streaming Read` as a example,

```sql
SET execution.runtime-mode = streaming;
SELECT * FROM sample /*+ OPTIONS('streaming'='true', 'monitor-interval'='1s')*/ ;
```

Taking `INSERT INTO` as a example,

```sql
INSERT INTO `hive_catalog`.`default`.`sample` VALUES (1, 'a');
INSERT INTO `hive_catalog`.`default`.`sample` SELECT id, data from other_kafka_table;
```

Taking `INSERT OVERWRITE` as a example, Flink streaming job does not support INSERT OVERWRITE.

```sql
INSERT OVERWRITE `hive_catalog`.`default`.`sample` VALUES (1, 'a');
INSERT OVERWRITE `hive_catalog`.`default`.`sample` PARTITION(data='a') SELECT 6;
```
