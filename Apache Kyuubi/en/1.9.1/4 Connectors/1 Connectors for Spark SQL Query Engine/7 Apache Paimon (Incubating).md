[TOC]

Apache Paimon(incubating) is a streaming data lake platform that supports high-speed data ingestion, change data tracking and efficient real-time analytics.

> This article assumes that you have mastered the basic knowledge and operation of [Apache Paimon (Incubating)](https://paimon.apache.org/). For the knowledge about Apache Paimon (Incubating) not mentioned in this article, you can obtain it from its [Official Documentation](https://paimon.apache.org/docs/master/).

By using kyuubi, we can run SQL queries towards Apache Paimon (Incubating) which is more convenient, easy to understand, and easy to expand than directly using spark to manipulate Apache Paimon (Incubating).

Apache Paimon (Incubating) Integration
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and Apache Paimon (Incubating), you need to set the following configurations:

*   Referencing the Apache Paimon (Incubating) [dependencies](#spark-paimon-deps)
*   Setting the spark extension and catalog [configurations](#spark-paimon-conf)

### Dependencies

The **classpath** of kyuubi spark sql engine with Apache Paimon (Incubating) consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of spark distribution
3.  paimon-spark-<version>.jar (example: paimon-spark-3.3-0.4-20230323.002035-5.jar), which can be found in the [Apache Paimon (Incubating) Supported Engines Spark3](https://paimon.apache.org/docs/master/engines/spark3/)

In order to make the Apache Paimon (Incubating) packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the Apache Paimon (Incubating) packages into `$SPARK_HOME/jars` directly
2.  Set `spark.jars=/path/to/paimon-spark-<version>.jar`

> Please mind the compatibility of different Apache Paimon (Incubating) and Spark versions, which can be confirmed on the page of [Apache Paimon (Incubating) multi engine support](https://paimon.apache.org/docs/master/engines/overview/).

### Configurations

To activate functionality of Apache Paimon (Incubating), we can set the following configurations:

```properties
spark.sql.catalog.paimon=org.apache.paimon.spark.SparkCatalog
spark.sql.catalog.paimon.warehouse=file:/tmp/paimon
```

Apache Paimon (Incubating) Operations[#](https://kyuubi.readthedocs.io/en/v1.9.1/connector/spark/paimon.html#apache-paimon-incubating-operations "Link to this heading")
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Taking `CREATE NAMESPACE` as a example,

```sql
CREATE DATABASE paimon.default;
USE paimon.default;
```

Taking `CREATE TABLE` as a example,

```sql
create table my_table (
    k int,
    v string
) tblproperties (
    'primary-key' = 'k'
);
```

Taking `SELECT` as a example,

```sql
SELECT * FROM my_table;
```

Taking `INSERT` as a example,

```sql
INSERT INTO my_table VALUES (1, 'Hi Again'), (3, 'Test');
```
