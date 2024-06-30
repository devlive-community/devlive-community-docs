[TOC]

To use Iceberg in Spark, first configure [Spark catalogs]($S-Configuration). Iceberg uses Apache Spark's DataSourceV2 API for data source and catalog implementations.

## `CREATE TABLE`

Spark 3 can create tables in any Iceberg catalog with the clause `USING iceberg`:

```sql
CREATE TABLE prod.db.sample (
                                id bigint NOT NULL COMMENT 'unique id',
                                data string)
    USING iceberg;
```

Iceberg will convert the column type in Spark to corresponding Iceberg type. Please check the section of [type compatibility on creating table]($Writes#spark-type-to-iceberg-type) for details.

Table create commands, including CTAS and RTAS, support the full range of Spark create clauses, including:

* `PARTITIONED BY (partition-expressions)` to configure partitioning
* `LOCATION '(fully-qualified-uri)'` to set the table location
* `COMMENT 'table documentation'` to set a table description
* `TBLPROPERTIES ('key'='value', ...)` to set [table configuration]($Configuration)

Create commands may also set the default format with the `USING` clause. This is only supported for `SparkCatalog` because Spark handles the `USING` clause differently for the built-in catalog.

`CREATE TABLE ... LIKE ...` syntax is not supported.

### `PARTITIONED BY`

To create a partitioned table, use `PARTITIONED BY`:

```sql
CREATE TABLE prod.db.sample (
    id bigint,
    data string,
    category string)
USING iceberg
PARTITIONED BY (category);
```

The `PARTITIONED BY` clause supports transform expressions to create [hidden partitions]($Partitioning).

```sql
CREATE TABLE prod.db.sample (
    id bigint,
    data string,
    category string,
    ts timestamp)
USING iceberg
PARTITIONED BY (bucket(16, id), days(ts), category);
```

Supported transformations are:

```sql
ALTER TABLE prod.db.sample WRITE LOCALLY ORDERED BY category, id
```

To unset the sort order of the table, use `UNORDERED`:

```sql
ALTER TABLE prod.db.sample WRITE UNORDERED
```

### `ALTER TABLE ... WRITE DISTRIBUTED BY PARTITION`

`WRITE DISTRIBUTED BY PARTITION` will request that each partition is handled by one writer, the default implementation is hash distribution.

```sql
ALTER TABLE prod.db.sample WRITE DISTRIBUTED BY PARTITION
```

`DISTRIBUTED BY PARTITION` and `LOCALLY ORDERED BY` may be used together, to distribute by partition and locally order rows within each task.

```sql
ALTER TABLE prod.db.sample WRITE DISTRIBUTED BY PARTITION LOCALLY ORDERED BY category, id
```

### `ALTER TABLE ... SET IDENTIFIER FIELDS`

Iceberg supports setting [identifier fields](https://iceberg.apache.org/spec/#identifier-field-ids) to a spec using `SET IDENTIFIER FIELDS`:
Spark table can support Flink SQL upsert operation if the table has identifier fields.

```sql
ALTER TABLE prod.db.sample SET IDENTIFIER FIELDS id
-- single column
ALTER TABLE prod.db.sample SET IDENTIFIER FIELDS id, data
-- multiple columns
```

Identifier fields must be `NOT NULL` columns when they are created or added.
The later `ALTER` statement will overwrite the previous setting.

### `ALTER TABLE ... DROP IDENTIFIER FIELDS`

Identifier fields can be removed using `DROP IDENTIFIER FIELDS`:

```sql
ALTER TABLE prod.db.sample DROP IDENTIFIER FIELDS id
-- single column
ALTER TABLE prod.db.sample DROP IDENTIFIER FIELDS id, data
-- multiple columns
```

Note that although the identifier is removed, the column will still exist in the table schema.

### Branching and Tagging DDL

#### `ALTER TABLE ... CREATE BRANCH`

Branches can be created via the `CREATE BRANCH` statement with the following options:
* Do not fail if the branch already exists with `IF NOT EXISTS`
* Update the branch if it already exists with `CREATE OR REPLACE`
* Create at a snapshot
* Create with retention

```sql
-- CREATE audit-branch at current snapshot with default retention.
ALTER TABLE prod.db.sample CREATE BRANCH `audit-branch`

-- CREATE audit-branch at current snapshot with default retention if it doesn't exist.
ALTER TABLE prod.db.sample CREATE BRANCH IF NOT EXISTS `audit-branch`

-- CREATE audit-branch at current snapshot with default retention or REPLACE it if it already exists.
ALTER TABLE prod.db.sample CREATE OR REPLACE BRANCH `audit-branch`

-- CREATE audit-branch at snapshot 1234 with default retention.
ALTER TABLE prod.db.sample CREATE BRANCH `audit-branch`
AS OF VERSION 1234

-- CREATE audit-branch at snapshot 1234, retain audit-branch for 31 days, and retain the latest 31 days. The latest 3 snapshot snapshots, and 2 days worth of snapshots. 
ALTER TABLE prod.db.sample CREATE BRANCH `audit-branch`
AS OF VERSION 1234 RETAIN 30 DAYS 
WITH SNAPSHOT RETENTION 3 SNAPSHOTS 2 DAYS
```

#### `ALTER TABLE ... CREATE TAG`

Tags can be created via the `CREATE TAG` statement with the following options:
* Do not fail if the tag already exists with `IF NOT EXISTS`
* Update the tag if it already exists with `CREATE OR REPLACE`
* Create at a snapshot
* Create with retention

```sql
-- CREATE historical-tag at current snapshot with default retention.
ALTER TABLE prod.db.sample CREATE TAG `historical-tag`

-- CREATE historical-tag at current snapshot with default retention if it doesn't exist.
ALTER TABLE prod.db.sample CREATE TAG IF NOT EXISTS `historical-tag`

-- CREATE historical-tag at current snapshot with default retention or REPLACE it if it already exists.
ALTER TABLE prod.db.sample CREATE OR REPLACE TAG `historical-tag`

-- CREATE historical-tag at snapshot 1234 with default retention.
ALTER TABLE prod.db.sample CREATE TAG `historical-tag` AS OF VERSION 1234

-- CREATE historical-tag at snapshot 1234 and retain it for 1 year. 
ALTER TABLE prod.db.sample CREATE TAG `historical-tag` 
AS OF VERSION 1234 RETAIN 365 DAYS
```

#### `ALTER TABLE ... REPLACE BRANCH`

The snapshot which a branch references can be updated via
the `REPLACE BRANCH` sql. Retention can also be updated in this statement.

```sql
-- REPLACE audit-branch to reference snapshot 4567 and update the retention to 60 days.
ALTER TABLE prod.db.sample REPLACE BRANCH `audit-branch`
AS OF VERSION 4567 RETAIN 60 DAYS
```

#### `ALTER TABLE ... REPLACE TAG`

The snapshot which a tag references can be updated via
the `REPLACE TAG` sql. Retention can also be updated in this statement.

```sql
-- REPLACE historical-tag to reference snapshot 4567 and update the retention to 60 days.
ALTER TABLE prod.db.sample REPLACE TAG `historical-tag`
AS OF VERSION 4567 RETAIN 60 DAYS
```

#### `ALTER TABLE ... DROP BRANCH`

Branches can be removed via the `DROP BRANCH` sql

```sql
ALTER TABLE prod.db.sample DROP BRANCH `audit-branch`
```

#### `ALTER TABLE ... DROP TAG`

Tags can be removed via the `DROP TAG` sql

```sql
ALTER TABLE prod.db.sample DROP TAG `historical-tag`
```