[TOC]

Apache Iceberg is an open table format for huge analytic datasets. Iceberg adds tables to compute engines including Spark, Trino, PrestoDB, Flink, Hive and Impala using a high-performance table format that works just like a SQL table.

> This article assumes that you have mastered the basic knowledge and operation of [Iceberg](https://iceberg.apache.org/). For the knowledge about Iceberg not mentioned in this article, you can obtain it from its [Official Documentation](https://trino.io/docs/current/connector/iceberg.html#).

By using kyuubi, we can run SQL queries towards Iceberg which is more convenient, easy to understand, and easy to expand than directly using Trino to manipulate Iceberg.

Iceberg Integration
---------------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi trino sql engine and Iceberg through Catalog APIs, you need to:

*   Setting the Trino extension and catalog [Configurations](#configurations)

### Configurations

To activate functionality of Iceberg, we can set the following configurations:

```properties
connector.name=iceberg
hive.metastore.uri=thrift://localhost:9083
```

Iceberg Operations
-------------------------------------------------------------------------------------------------------------------------------------

Taking `CREATE TABLE` as a example,

```sql
CREATE TABLE orders (
  orderkey bigint,
  orderstatus varchar,
  totalprice double,
  orderdate date
) WITH (
  format = 'ORC'
);
```

Taking `SELECT` as a example,

```sql
SELECT * FROM new_orders;
```

Taking `INSERT` as a example,

```sql
INSERT INTO cities VALUES (1, 'San Francisco');
```

Taking `UPDATE` as a example,

```sql
UPDATE purchases SET status = 'OVERDUE' WHERE ship_date IS NULL;
```

Taking `DELETE FROM` as a example,

```sql
DELETE FROM lineitem WHERE shipmode = 'AIR';
```
