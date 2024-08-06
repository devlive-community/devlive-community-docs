[TOC]

Apache Hudi (pronounced “hoodie”) is the next generation streaming data lake platform. Apache Hudi brings core warehouse and database functionality directly to a data lake.

> This article assumes that you have mastered the basic knowledge and operation of [Hudi](https://hudi.apache.org/). For the knowledge about Hudi not mentioned in this article, you can obtain it from its [Official Documentation](https://hudi.apache.org/docs/overview).

By using Kyuubi, we can run SQL queries towards Hudi which is more convenient, easy to understand, and easy to expand than directly using Trino to manipulate Hudi.

Hudi Integration
------------------------------------------------------------------------------------------------------------------------------

To enable the integration of Kyuubi Trino SQL engine and Hudi, you need to:

*   Setting the Trino extension and catalog [configurations](#trino-hudi-conf)

### Configurations

Catalogs are registered by creating a file of catalog properties in the $TRINO_SERVER_HOME/etc/catalog directory. For example, we can create a $TRINO_SERVER_HOME/etc/catalog/hudi.properties with the following contents to mount the Hudi connector as a Hudi catalog:

```properties
connector.name=hudi
hive.metastore.uri=thrift://example.net:9083
```

Note: You need to replace $TRINO_SERVER_HOME above to your Trino server home path like /opt/trino-server-406.

More configuration properties can be found in the [Hudi connector in Trino document](https://trino.io/docs/current/connector/hudi.html).

> Trino version 398 or higher, it is recommended to use the Hudi connector. You don’t need to install any dependencies in version 398 or higher.

Hudi Operations
----------------------------------------------------------------------------------------------------------------------------

The globally available and read operation statements are supported in Trino. These statements can be found in [Trino SQL Support](https://trino.io/docs/current/language/sql-support.html#). Currently, Trino cannot write data to a Hudi table. A common scenario is to write data with Spark/Flink and read data with Trino. You can use the Kyuubi Trino SQL engine to query the table with the following SQL `SELECT` statement.

Taking `Query Data` as a example,

USE example.example\_schema;

```sql
USE example.example_schema;

SELECT symbol, max(ts)
FROM stock_ticks_cow
GROUP BY symbol
HAVING symbol = 'GOOG';
```
