[TOC]

Apache Hudi (pronounced “hoodie”) is the next generation streaming data lake platform. Apache Hudi brings core warehouse and database functionality directly to a data lake.

> This article assumes that you have mastered the basic knowledge and operation of [Hudi](https://hudi.apache.org/). For the knowledge about Hudi not mentioned in this article, you can obtain it from its [Official Documentation](https://hudi.apache.org/docs/overview).

By using Kyuubi, we can run SQL queries towards Hudi which is more convenient, easy to understand, and easy to expand than directly using flink to manipulate Hudi.

Hudi Integration
------------------------------------------------------------------------------------------------------------------------------

To enable the integration of kyuubi flink sql engine and Hudi through Catalog APIs, you need to:

*   Referencing the Hudi [dependencies](#flink-hudi-deps)

### Dependencies

The **classpath** of kyuubi flink sql engine with Hudi supported consists of

1.  kyuubi-flink-sql-engine-1.9.1_2.12.jar, the engine jar deployed with Kyuubi distributions
2.  a copy of flink distribution
3.  hudi-flink<flink.version>-bundle_<scala.version>-<hudi.version>.jar (example: hudi-flink1.14-bundle\_2.12-0.11.1.jar), which can be found in the [Maven Central](https://mvnrepository.com/artifact/org.apache.hudi)

In order to make the Hudi packages visible for the runtime classpath of engines, we can use one of these methods:

1.  Put the Hudi packages into `$flink_HOME/lib` directly
2.  Set `pipeline.jars=/path/to/hudi-flink-bundle`

Hudi Operations
----------------------------------------------------------------------------------------------------------------------------

Taking `Create Table` as a example,

```sql
CREATE TABLE t1 (
  id INT PRIMARY KEY NOT ENFORCED,
  name STRING,
  price DOUBLE
) WITH (
  'connector' = 'hudi',
  'path' = 's3://bucket-name/hudi/',
  'table.type' = 'MERGE_ON_READ' -- this creates a MERGE_ON_READ table, by default is COPY_ON_WRITE
);
```

Taking `Query Data` as a example,

```sql
SELECT * FROM t1;
```

Taking `Insert and Update Data` as a example,

```sql
INSERT INTO t1 VALUES (1, 'Lucas' , 2.71828);
```

Taking `Streaming Query` as a example,

```sql
CREATE TABLE t1 (
  uuid VARCHAR(20) PRIMARY KEY NOT ENFORCED,
  name VARCHAR(10),
  age INT,
  ts TIMESTAMP(3),
  `partition` VARCHAR(20)
)
PARTITIONED BY (`partition`)
WITH (
  'connector' = 'hudi',
  'path' = '${path}',
  'table.type' = 'MERGE_ON_READ',
  'read.streaming.enabled' = 'true',  -- this option enable the streaming read
  'read.start-commit' = '20210316134557', -- specifies the start commit instant time
  'read.streaming.check-interval' = '4' -- specifies the check interval for finding new source commits, default 60s.
);

-- Then query the table in stream mode
SELECT * FROM t1;
```

Taking `Delete Data`,

The streaming query can implicitly auto delete data. When consuming data in streaming query, Hudi Flink source can also accepts the change logs from the underneath data source, it can then applies the UPDATE and DELETE by per-row level.

