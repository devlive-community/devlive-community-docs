[TOC]

Apache Hudi (pronounced “hoodie”) is the next generation streaming data lake platform. Apache Hudi brings core warehouse and database functionality directly to a data lake.

> This article assumes that you have mastered the basic knowledge and operation of [Hudi](https://hudi.apache.org/). For the knowledge about Hudi not mentioned in this article, you can obtain it from its [Official Documentation](https://hudi.apache.org/docs/overview).

By using Kyuubi, we can run SQL queries towards Hudi which is more convenient, easy to understand, and easy to expand than directly using Spark to manipulate Hudi.

Hudi Integration
------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and Hudi through Catalog APIs, you need to:

*   Referencing the Hudi [dependencies](#spark-hudi-deps)
*   Setting the Spark extension and catalog [configurations](#spark-hudi-conf)


### Dependencies

The **classpath** of kyuubi spark sql engine with Hudi supported consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of spark distribution
3.  hudi-spark<spark.version>-bundle_<scala.version>-<hudi.version>.jar (example: hudi-spark3.2-bundle\_2.12-0.11.1.jar), which can be found in the [Maven Central](https://mvnrepository.com/artifact/org.apache.hudi)

In order to make the Hudi packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the Hudi packages into `$SPARK_HOME/jars` directly
2.  Set `spark.jars=/path/to/hudi-spark-bundle`

### Configurations

To activate functionality of Hudi, we can set the following configurations:

```bash
# Spark 3.2
spark.serializer=org.apache.spark.serializer.KryoSerializer
spark.sql.extensions=org.apache.spark.sql.hudi.HoodieSparkSessionExtension
spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog

# Spark 3.1
spark.serializer=org.apache.spark.serializer.KryoSerializer
spark.sql.extensions=org.apache.spark.sql.hudi.HoodieSparkSessionExtension
```

Hudi Operations
----------------------------------------------------------------------------------------------------------------------------

Taking `Create Table` as a example,

```sql
CREATE TABLE hudi_cow_nonpcf_tbl (
  uuid INT,
  name STRING,
  price DOUBLE
) USING HUDI;
```

Taking `Query Data` as a example,

```sql
SELECT * FROM hudi_cow_nonpcf_tbl WHERE id < 20;
```

Taking `Insert Data` as a example,

```sql
INSERT INTO hudi_cow_nonpcf_tbl SELECT 1, 'a1', 20;
```

Taking `Update Data` as a example,

```sql
UPDATE hudi_cow_nonpcf_tbl SET name = 'foo', price = price * 2 WHERE id = 1;
```

Taking `Delete Data` as a example,

```sql
DELETE FROM hudi_cow_nonpcf_tbl WHERE uuid = 1;
```
