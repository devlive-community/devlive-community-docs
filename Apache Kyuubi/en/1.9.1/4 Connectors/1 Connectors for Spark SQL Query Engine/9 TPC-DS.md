[TOC]

The TPC-DS is a decision support benchmark. It consists of a suite of business oriented ad-hoc queries and concurrent data modifications. The queries and the data populating the database have been chosen to have broad industry-wide relevance.

> This article assumes that you have mastered the basic knowledge and operation of [TPC-DS](https://kyuubi.readthedocs.io/en/v1.9.1/connector/spark/tpcds.html#tpc-ds). For the knowledge about TPC-DS not mentioned in this article, you can obtain it from its [Official Documentation](https://www.tpc.org/tpcds/).

This connector can be used to test the capabilities and query syntax of Spark without configuring access to an external data source. When you query a TPC-DS table, the connector generates the data on the fly using a deterministic algorithm.

Goto [Try Kyuubi](https://try.kyuubi.cloud/) to explore TPC-DS data instantly!

TPC-DS Integration
-----------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and TPC-DS through Apache Spark Datasource V2 and Catalog APIs, you need to:

*   Referencing the TPC-DS connector [dependencies](#spark-tpcds-deps)
*   Setting the spark catalog [configurations](#spark-tpcds-conf)

### Dependencies

The **classpath** of kyuubi spark sql engine with TPC-DS supported consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of spark distribution
3.  kyuubi-spark-connector-tpcds-1.9.1_2.12.jar, which can be found in the [Maven Central](https://repo1.maven.org/maven2/org/apache/kyuubi/kyuubi-spark-connector-tpcds_2.12/)

In order to make the TPC-DS connector package visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the TPC-DS connector package into `$SPARK_HOME/jars` directly
2.  Set spark.jars=kyuubi-spark-connector-tpcds-1.9.1_2.12.jar

### Configurations

To add TPC-DS tables as a catalog, we can set the following configurations in `$SPARK_HOME/conf/spark-defaults.conf`:

```properties
# (required) Register a catalog named `tpcds` for the spark engine.
spark.sql.catalog.tpcds=org.apache.kyuubi.spark.connector.tpcds.TPCDSCatalog

# (optional) Excluded database list from the catalog, all available databases are:
#            sf0, tiny, sf1, sf10, sf30, sf100, sf300, sf1000, sf3000, sf10000, sf30000, sf100000.
spark.sql.catalog.tpcds.excludeDatabases=sf10000,sf30000

# (optional) When true, use CHAR/VARCHAR, otherwise use STRING. It affects output of the table schema,
#            e.g. `SHOW CREATE TABLE <table>`, `DESC <table>`.
spark.sql.catalog.tpcds.useAnsiStringType=false

# (optional) TPCDS changed table schemas in v2.6.0, turn off this option to use old table schemas.
#            See detail at: https://www.tpc.org/tpc_documents_current_versions/pdf/tpc-ds_v3.2.0.pdf
spark.sql.catalog.tpcds.useTableSchema_2_6=true

# (optional) Maximum bytes per task, consider reducing it if you want higher parallelism.
spark.sql.catalog.tpcds.read.maxPartitionBytes=128m
```

TPC-DS Operations
---------------------------------------------------------------------------------------------------------------------------------

Listing databases under tpcds catalog.

```sql
SHOW DATABASES IN tpcds;
```

Listing tables under tpcds.sf1 database.

```sql
SHOW TABLES IN tpcds.sf1;
```

Switch current database to tpcds.sf1 and run a query against it.

```sql
USE tpcds.sf1;
SELECT * FROM store;
```
