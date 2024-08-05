[TOC]

Apache Paimon (Incubating) is a streaming data lake platform that supports high-speed data ingestion, change data tracking, and efficient real-time analytics.

> This article assumes that you have mastered the basic knowledge and operation of [Apache Paimon (Incubating)](https://paimon.apache.org/). For the knowledge not mentioned in this article, you can obtain it from its [Official Documentation](https://paimon.apache.org/docs/master/).

By using kyuubi, we can run SQL queries towards Apache Paimon (Incubating) which is more convenient, easy to understand, and easy to expand than directly using flink.

Apache Paimon (Incubating) Integration
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi flink sql engine and Apache Paimon (Incubating), you need to:

*   Referencing the Apache Paimon (Incubating) [dependencies](#flink-paimon-deps)

### Dependencies

The **classpath** of kyuubi flink sql engine with Apache Paimon (Incubating) supported consists of

1.  kyuubi-flink-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of flink distribution
3.  paimon-flink-<version>.jar (example: paimon-flink-1.16-0.4-SNAPSHOT.jar), which can be found in the [Apache Paimon (Incubating) Supported Engines Flink](https://paimon.apache.org/docs/master/engines/flink/#preparing-paimon-jar-file)
4.  flink-shaded-hadoop-2-uber-<version>.jar, which code can be found in the [Pre-bundled Hadoop Jar](https://flink.apache.org/downloads/#additional-components)

In order to make the Apache Paimon (Incubating) packages visible for the runtime classpath of engines, you need to:

1.  Put the Apache Paimon (Incubating) packages into `$FLINK_HOME/lib` directly
2.  Setting the HADOOP_CLASSPATH environment variable or copy the [Pre-bundled Hadoop Jar](https://flink.apache.org/downloads/#additional-components) to flink/lib.

> Please mind the compatibility of different Apache Paimon (Incubating) and Flink versions, which can be confirmed on the page of [Apache Paimon (Incubating) multi engine support](https://paimon.apache.org/docs/master/engines/overview/).

Apache Paimon (Incubating) Operations
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Taking `CREATE CATALOG` as a example,

```sql
CREATE CATALOG my_catalog WITH (
    'type'='paimon',
    'warehouse'='file:/tmp/paimon'
);

USE CATALOG my_catalog;
```

Taking `CREATE TABLE` as a example,

```sql
CREATE TABLE MyTable (
  user_id BIGINT,
  item_id BIGINT,
  behavior STRING,
  dt STRING,
  PRIMARY KEY (dt, user_id) NOT ENFORCED
) PARTITIONED BY (dt) WITH (
  'bucket' = '4'
);
```

Taking `Query Table` as a example,

```sql
SET 'execution.runtime-mode' = 'batch';
SELECT * FROM orders WHERE catalog_id=1025;
```

Taking `Streaming Query` as a example,

```sql
SET 'execution.runtime-mode' = 'streaming';
SELECT * FROM MyTable /*+ OPTIONS ('log.scan'='latest') */;
```

Taking `Rescale Bucket` as a example,

```sql
ALTER TABLE my_table SET ('bucket' = '4');
INSERT OVERWRITE my_table PARTITION (dt = '2022-01-01');
```
