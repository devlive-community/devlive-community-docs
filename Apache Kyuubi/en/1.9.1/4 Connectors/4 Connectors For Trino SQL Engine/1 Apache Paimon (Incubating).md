[TOC]

Apache Paimon(incubating) is a streaming data lake platform that supports high-speed data ingestion, change data tracking and efficient real-time analytics.

> This article assumes that you have mastered the basic knowledge and operation of [Apache Paimon (Incubating)](https://paimon.apache.org/). For the knowledge about Apache Paimon (Incubating) not mentioned in this article, you can obtain it from its [Official Documentation](https://paimon.apache.org/docs/master/).

By using kyuubi, we can run SQL queries towards Apache Paimon (Incubating) which is more convenient, easy to understand, and easy to expand than directly using trino to manipulate Apache Paimon (Incubating).

Apache Paimon (Incubating) Integration
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi trino sql engine and Apache Paimon (Incubating), you need to:

*   Referencing the Apache Paimon (Incubating) [dependencies](#trino-paimon-deps)
*   Setting the trino extension and catalog [configurations](#trino-paimon-conf)

### Dependencies

The **classpath** of kyuubi trino sql engine with Apache Paimon (Incubating) supported consists of

1.  kyuubi-trino-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of trino distribution
3.  paimon-trino-<version>.jar (example: paimon-trino-0.2.jar), which code can be found in the [Source Code](https://github.com/JingsongLi/paimon-trino)
4.  flink-shaded-hadoop-2-uber-<version>.jar, which code can be found in the [Pre-bundled Hadoop](https://flink.apache.org/downloads/#additional-components)

In order to make the Apache Paimon (Incubating) packages visible for the runtime classpath of engines, you need to:

1.  Build the paimon-trino-<version>.jar by reference to [Apache Paimon (Incubating) Trino README](https://github.com/JingsongLi/paimon-trino#readme)
2.  Put the paimon-trino-<version>.jar and flink-shaded-hadoop-2-uber-<version>.jar packages into `$TRINO_SERVER_HOME/plugin/tablestore` directly

> Please mind the compatibility of different Apache Paimon (Incubating) and Trino versions, which can be confirmed on the page of [Apache Paimon (Incubating) multi engine support](https://paimon.apache.org/docs/master/engines/overview/).

### Configurations

To activate functionality of Apache Paimon (Incubating), we can set the following configurations:

Catalogs are registered by creating a catalog properties file in the $TRINO_SERVER_HOME/etc/catalog directory. For example, create $TRINO_SERVER_HOME/etc/catalog/tablestore.properties with the following contents to mount the tablestore connector as the tablestore catalog:

```properties
connector.name=tablestore
warehouse=file:///tmp/warehouse
```

Apache Paimon (Incubating) Operations
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Apache Paimon (Incubating) supports reading table store tables through Trino. A common scenario is to write data with Spark or Flink and read data with Trino. You can follow this document [Apache Paimon (Incubating) Engines Flink Quick Start](https://paimon.apache.org/docs/master/engines/flink/#quick-start) to write data to a table store table and then use kyuubi trino sql engine to query the table with the following SQL `SELECT` statement.

```sql
SELECT * FROM tablestore.default.t1
```
