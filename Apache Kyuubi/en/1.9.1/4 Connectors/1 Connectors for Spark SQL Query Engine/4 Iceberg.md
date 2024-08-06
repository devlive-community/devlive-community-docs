[TOC]

Apache Iceberg is an open table format for huge analytic datasets. Iceberg adds tables to compute engines including Spark, Trino, PrestoDB, Flink, Hive and Impala using a high-performance table format that works just like a SQL table.

> This article assumes that you have mastered the basic knowledge and operation of [Iceberg](https://iceberg.apache.org/). For the knowledge about Iceberg not mentioned in this article, you can obtain it from its [Official Documentation](https://iceberg.apache.org/docs/latest/).

By using kyuubi, we can run SQL queries towards Iceberg which is more convenient, easy to understand, and easy to expand than directly using spark to manipulate Iceberg.

Iceberg Integration
---------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and Iceberg through Apache Spark Datasource V2 and Catalog APIs, you need to:

*   Referencing the Iceberg [dependencies](#spark-iceberg-deps)
*   Setting the spark extension and catalog [configurations](#spark-iceberg-conf)

### Dependencies

The **classpath** of kyuubi spark sql engine with Iceberg supported consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of spark distribution
3.  iceberg-spark-runtime-<spark.version>_<scala.version>-<iceberg.version>.jar (example: iceberg-spark-runtime-3.2\_2.12-0.14.0.jar), which can be found in the [Maven Central](https://mvnrepository.com/artifact/org.apache.iceberg)


In order to make the Iceberg packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the Iceberg packages into `$SPARK_HOME/jars` directly
2.  Set `spark.jars=/path/to/iceberg-spark-runtime`

> Please mind the compatibility of different Iceberg and Spark versions, which can be confirmed on the page of [Iceberg multi engine support](https://iceberg.apache.org/multi-engine-support/).

### Configurations

To activate functionality of Iceberg, we can set the following configurations:

```properties
spark.sql.catalog.spark_catalog=org.apache.iceberg.spark.SparkCatalog
spark.sql.catalog.spark_catalog.type=hive
spark.sql.catalog.spark_catalog.uri=thrift://metastore-host:port
spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions
```

Iceberg Operations
-------------------------------------------------------------------------------------------------------------------------------------

Taking `CREATE TABLE` as a example,

```sql
CREATE TABLE foo (
  id bigint COMMENT 'unique id',
  data string)
USING iceberg;
```

Taking `SELECT` as a example,

```sql
SELECT * FROM foo;
```

Taking `INSERT` as a example,

```sql
INSERT INTO foo VALUES (1, 'a'), (2, 'b'), (3, 'c');
```

Taking `UPDATE` as a example, Spark 3.1 added support for UPDATE queries that update matching rows in tables.

```sql
UPDATE foo SET data = 'd', id = 4 WHERE id >= 3 and id < 4;
```

Taking `DELETE FROM` as a example, Spark 3 added support for DELETE FROM queries to remove data from tables.

```sql
DELETE FROM foo WHERE id >= 1 and id < 2;
```

Taking `MERGE INTO` as a example,

```sql
MERGE INTO target_table t
USING source_table s
ON t.id = s.id
WHEN MATCHED AND s.opType = 'delete' THEN DELETE
WHEN MATCHED AND s.opType = 'update' THEN UPDATE SET id = s.id, data = s.data
WHEN NOT MATCHED AND s.opType = 'insert' THEN INSERT (id, data) VALUES (s.id, s.data);
```
