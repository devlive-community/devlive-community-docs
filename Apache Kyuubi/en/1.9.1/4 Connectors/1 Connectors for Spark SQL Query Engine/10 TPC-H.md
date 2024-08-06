[TOC]

The TPC-H is a decision support benchmark. It consists of a suite of business oriented ad-hoc queries and concurrent data modifications. The queries and the data populating the database have been chosen to have broad industry-wide relevance.

> This article assumes that you have mastered the basic knowledge and operation of [TPC-H](https://kyuubi.readthedocs.io/en/v1.9.1/connector/spark/tpch.html#tpc-h). For the knowledge about TPC-H not mentioned in this article, you can obtain it from its [Official Documentation](https://www.tpc.org/tpch/).

This connector can be used to test the capabilities and query syntax of Spark without configuring access to an external data source. When you query a TPC-H table, the connector generates the data on the fly using a deterministic algorithm.

Goto [Try Kyuubi](https://try.kyuubi.cloud/) to explore TPC-H data instantly!

TPC-H Integration
--------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi spark sql engine and TPC-H through Apache Spark Datasource V2 and Catalog APIs, you need to:

*   Referencing the TPC-H connector [dependencies](#spark-tpch-deps)
*   Setting the spark catalog [configurations](#spark-tpch-conf)

### Dependencies

The **classpath** of kyuubi spark sql engine with TPC-H supported consists of

1.  kyuubi-spark-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of spark distribution
3.  kyuubi-spark-connector-tpch-1.9.1_2.12.jar, which can be found in the [Maven Central](https://repo1.maven.org/maven2/org/apache/kyuubi/kyuubi-spark-connector-tpch_2.12/)

In order to make the TPC-H connector package visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the TPC-H connector package into `$SPARK_HOME/jars` directly
2.  Set spark.jars=kyuubi-spark-connector-tpch-1.9.1_2.12.jar

### Configurations

To add TPC-H tables as a catalog, we can set the following configurations in `$SPARK_HOME/conf/spark-defaults.conf`:

```properties
# (required) Register a catalog named `tpch` for the spark engine.
spark.sql.catalog.tpch=org.apache.kyuubi.spark.connector.tpch.TPCHCatalog

# (optional) Excluded database list from the catalog, all available databases are:
#            sf0, tiny, sf1, sf10, sf30, sf100, sf300, sf1000, sf3000, sf10000, sf30000, sf100000.
spark.sql.catalog.tpch.excludeDatabases=sf10000,sf30000

# (optional) When true, use CHAR/VARCHAR, otherwise use STRING. It affects output of the table schema,
#            e.g. `SHOW CREATE TABLE <table>`, `DESC <table>`.
spark.sql.catalog.tpch.useAnsiStringType=false

# (optional) Maximum bytes per task, consider reducing it if you want higher parallelism.
spark.sql.catalog.tpch.read.maxPartitionBytes=128m
```

TPC-H Operations
------------------------------------------------------------------------------------------------------------------------------

Listing databases under tpch catalog.

```sql
SHOW DATABASES IN tpch;
```

Listing tables under tpch.sf1 database.

```sql
SHOW TABLES IN tpch.sf1;
```

Switch current database to tpch.sf1 and run a query against it.

```sql
USE tpch.sf1;
SELECT * FROM orders;
```
