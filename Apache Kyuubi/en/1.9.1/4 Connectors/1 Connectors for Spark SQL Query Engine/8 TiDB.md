[TOC]

TiDB is an open-source NewSQL database that supports Hybrid Transactional and Analytical Processing (HTAP) workloads.

TiSpark is a thin layer built for running Apache Spark on top of TiDB/TiKV to answer complex OLAP queries. It enjoys the merits of both the Spark platform and the distributed clusters of TiKV while seamlessly integrated to TiDB to provide one-stop HTAP solutions for online transactions and analyses.

> This article assumes that you have mastered the basic knowledge and operation of TiDB and TiSpark. For the knowledge not mentioned in this article, you can obtain it from TiDB [Official Documentation](https://docs.pingcap.com/tidb/stable/overview).

By using kyuubi, we can run SQL queries towards TiDB/TiKV which is more convenient, easy to understand, and easy to expand than directly using spark to manipulate TiDB/TiKV.

TiDB Integration
------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and TiDB through Apache Spark Datasource V2 and Catalog APIs, you need to:

*   Referencing the TiSpark [dependencies](#spark-tidb-deps)
*   Setting the spark extension and catalog [configurations](#spark-tidb-conf)

### Dependencies

The classpath of kyuubi spark sql engine with TiDB supported consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of spark distribution
3.  tispark-assembly-<spark.version>_<scala.version>-<tispark.version>.jar (example: tispark-assembly-3.2\_2.12-3.0.1.jar), which can be found in the [Maven Central](https://repo1.maven.org/maven2/com/pingcap/tispark/)

In order to make the TiSpark packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the TiSpark packages into `$SPARK_HOME/jars` directly
2.  Set `spark.jars=/path/to/tispark-assembly`

> Please mind the compatibility of different TiDB, TiSpark and Spark versions, which can be confirmed on the page of [TiSpark Environment setup](https://docs.pingcap.com/tidb/stable/tispark-overview#environment-setup).

### Configurations

To activate functionality of TiSpark, we can set the following configurations:

```properties
spark.tispark.pd.addresses $pd_host:$pd_port
spark.sql.extensions org.apache.spark.sql.TiExtensions
spark.sql.catalog.tidb_catalog  org.apache.spark.sql.catalyst.catalog.TiCatalog
spark.sql.catalog.tidb_catalog.pd.addresses $pd_host:$pd_port
```

The **spark.tispark.pd.addresses** and **spark.sql.catalog.tidb_catalog.pd.addresses** configurations allow you to put in multiple PD servers. Specify the port number for each of them.

For example, when you have multiple PD servers on **10.16.20.1**,**10.16.20.2**,**10.16.20.3** with the port **2379**, put it as **10.16.20.1:2379**,**10.16.20.2:2379**,**10.16.20.3:2379**.

TiDB Operations
----------------------------------------------------------------------------------------------------------------------------

Taking `SELECT` as a example,

```sql
SELECT * FROM foo;
```

Taking `DELETE FROM` as a example, Spark 3 added support for DELETE FROM queries to remove data from tables.

```sql
DELETE FROM foo WHERE id >= 1 and id < 2;
```

> As for now (TiSpark 3.0.1), TiSpark does not support `CREATE TABLE`, `INSERT INTO/OVERWRITE` operations through Apache Spark Datasource V2 and Catalog APIs.
