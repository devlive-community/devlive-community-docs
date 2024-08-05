[TOC]

Delta lake is an open-source project that enables building a Lakehouse Architecture on top of existing storage systems such as S3, ADLS, GCS, and HDFS.

> This article assumes that you have mastered the basic knowledge and operation of [Delta Lake](https://delta.io/). For the knowledge about delta lake not mentioned in this article, you can obtain it from its [Official Documentation](https://docs.delta.io/latest/index.html).

By using kyuubi, we can run SQL queries towards delta lake which is more convenient, easy to understand, and easy to expand than directly using spark to manipulate delta lake.

Delta Lake Integration
------------------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and delta lake through Apache Spark Datasource V2 and Catalog APIs, you need to:

*   Referencing the delta lake [dependencies](#spark-delta-lake-deps)
*   Setting the spark extension and catalog [configurations](#spark-delta-lake-conf)

### Dependencies

The **classpath** of kyuubi spark sql engine with delta lake supported consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with kyuubi distributions
2.  a copy of spark distribution
3.  delta-core & delta-storage, which can be found in the [Maven Central](https://mvnrepository.com/artifact/io.delta/delta-core)

In order to make the delta packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the delta packages into `$SPARK_HOME/jars` directly
2.  Set `spark.jars=/path/to/delta-core,/path/to/delta-storage`

> Please mind the compatibility of different Delta Lake and Spark versions, which can be confirmed on the page of [delta release notes](https://github.com/delta-io/delta/releases).

### Configurations

To activate functionality of delta lake, we can set the following configurations:

```properties
spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension
spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog
```

Delta Lake Operations
----------------------------------------------------------------------------------------------------------------------------------------------

As for end-users, who only use a pure SQL interface, there aren’t much differences between using a delta table and a regular hive table. Unless you are going to use some advanced features, but they are still SQL, just more syntax added.

Taking `CREATE A TABLE` as a example,

```sql
CREATE TABLE IF NOT EXISTS kyuubi_delta (
  id INT,
  name STRING,
  org STRING,
  url STRING,
  start TIMESTAMP
) USING DELTA;
```
