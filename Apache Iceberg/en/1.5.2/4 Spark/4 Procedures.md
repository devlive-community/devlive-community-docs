[TOC]

To use Iceberg in Spark, first configure [Spark catalogs]($S-Configuration). Stored procedures are only available when using [Iceberg SQL extensions]($S-Configuration#sql-extensions) in Spark 3.

## Usage

Procedures can be used from any configured Iceberg catalog with `CALL`. All procedures are in the namespace `system`.

`CALL` supports passing arguments by name (recommended) or by position. Mixing position and named arguments is not supported.

### Named arguments

All procedure arguments are named. When passing arguments by name, arguments can be in any order and any optional argument can be omitted.

```sql
CALL catalog_name.system.procedure_name(arg_name_2 => arg_2, arg_name_1 => arg_1);
```

### Positional arguments

When passing arguments by position, only the ending arguments may be omitted if they are optional.

```sql
CALL catalog_name.system.procedure_name(arg_1, arg_2, ... arg_n);
```

## Snapshot management

### `rollback_to_snapshot`

Roll back a table to a specific snapshot ID.

To roll back to a specific time, use [`rollback_to_timestamp`](#rollback_to_timestamp).

> This procedure invalidates all cached Spark plans that reference the affected table.


#### Usage

| Argument Name | Required? | Type | Description |
|---------------|-----------|------|-------------|
| `table`       | ✔️  | string | Name of the table to update |
| `snapshot_id` | ✔️  | long   | Snapshot ID to rollback to |

#### Output

| Output Name | Type | Description |
| ------------|------|-------------|
| `previous_snapshot_id` | long | The current snapshot ID before the rollback |
| `current_snapshot_id`  | long | The new current snapshot ID |

#### Example

Roll back table `db.sample` to snapshot ID `1`:
```sql
CALL spark_catalog.system.ancestors_of('db.tbl');
```

Get all the snapshot ancestors by a particular snapshot
```sql
CALL spark_catalog.system.ancestors_of('db.tbl', 1);
CALL spark_catalog.system.ancestors_of(snapshot_id => 1, table => 'db.tbl');
```

## Change Data Capture

### `create_changelog_view`

Creates a view that contains the changes from a given table.

#### Usage

| Argument Name        | Required? | Type                | Description                                                                                                                                                                                          |
|----------------------|-----------|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `table`              | ✔️         | string              | Name of the source table for the changelog                                                                                                                                                           |
| `changelog_view`     |           | string              | Name of the view to create                                                                                                                                                                           |
| `options`            |           | map<string, string> | A map of Spark read options to use                                                                                                                                                                   |
| `net_changes`        |           | boolean             | Whether to output net changes (see below for more information). Defaults to false.                                                                                                                   |
| `compute_updates`    |           | boolean             | Whether to compute pre/post update images (see below for more information). Defaults to false.                                                                                                       | 
| `identifier_columns` |           | array<string>       | The list of identifier columns to compute updates. If the argument `compute_updates` is set to true and `identifier_columns` are not provided, the table’s current identifier fields will be used.   |

Here is a list of commonly used Spark read options:

* `start-snapshot-id`: the exclusive start snapshot ID. If not provided, it reads from the table’s first snapshot inclusively.
* `end-snapshot-id`: the inclusive end snapshot id, default to table's current snapshot.
* `start-timestamp`: the exclusive start timestamp. If not provided, it reads from the table’s first snapshot inclusively.
* `end-timestamp`: the inclusive end timestamp, default to table's current snapshot.

#### Output
| Output Name | Type | Description                            |
| ------------|------|----------------------------------------|
| `changelog_view` | string | The name of the created changelog view |

#### Examples

Create a changelog view `tbl_changes` based on the changes that happened between snapshot `1` (exclusive) and `2` (inclusive).
```sql
CALL spark_catalog.system.create_changelog_view(
  table => 'db.tbl',
  options => map('start-snapshot-id','1','end-snapshot-id', '2')
);
```

Create a changelog view `my_changelog_view` based on the changes that happened between timestamp `1678335750489` (exclusive) and `1678992105265` (inclusive).
```sql
CALL spark_catalog.system.create_changelog_view(
  table => 'db.tbl',
  options => map('start-timestamp','1678335750489','end-timestamp', '1678992105265'),
  changelog_view => 'my_changelog_view'
);
```

Create a changelog view that computes updates based on the identifier columns `id` and `name`.
```sql
CALL spark_catalog.system.create_changelog_view(
  table => 'db.tbl',
  options => map('start-snapshot-id','1','end-snapshot-id', '2'),
  identifier_columns => array('id', 'name')
)
```

Once the changelog view is created, you can query the view to see the changes that happened between the snapshots.
```sql
SELECT * FROM tbl_changes;
```
```sql
SELECT * FROM tbl_changes where _change_type = 'INSERT' AND id = 3 ORDER BY _change_ordinal;
``` 
Please note that the changelog view includes Change Data Capture(CDC) metadata columns
that provide additional information about the changes being tracked. These columns are:

- `_change_type`: the type of change. It has one of the following values: `INSERT`, `DELETE`, `UPDATE_BEFORE`, or `UPDATE_AFTER`.
- `_change_ordinal`: the order of changes
- `_commit_snapshot_id`: the snapshot ID where the change occurred

Here is an example of corresponding results. It shows that the first snapshot inserted 2 records, and the
second snapshot deleted 1 record.

|  id	| name	  |_change_type |	_change_ordinal	| _change_snapshot_id |
|---|--------|---|---|---|
|1	| Alice	 |INSERT	|0	|5390529835796506035|
|2	| Bob	   |INSERT	|0	|5390529835796506035|
|1	| Alice  |DELETE	|1	|8764748981452218370|

Create a changelog view that computes net changes. It removes intermediate changes and only outputs the net changes.
```sql
CALL spark_catalog.system.create_changelog_view(
  table => 'db.tbl',
  options => map('end-snapshot-id', '87647489814522183702'),
  net_changes => true
);
```

With the net changes, the above changelog view only contains the following row since Alice was inserted in the first snapshot and deleted in the second snapshot.

|  id	| name	  |_change_type |	_change_ordinal	| _change_snapshot_id |
|---|--------|---|---|---|
|2	| Bob	   |INSERT	|0	|5390529835796506035|

#### Carry-over Rows

The procedure removes the carry-over rows by default. Carry-over rows are the result of row-level operations(`MERGE`, `UPDATE` and `DELETE`)
when using copy-on-write. For example, given a file which contains row1 `(id=1, name='Alice')` and row2 `(id=2, name='Bob')`.
A copy-on-write delete of row2 would require erasing this file and preserving row1 in a new file. The changelog table
reports this as the following pair of rows, despite it not being an actual change to the table.

| id  | name  | _change_type |
|-----|-------|--------------|
| 1   | Alice | DELETE       |
| 1   | Alice | INSERT       |

To see carry-over rows, query `SparkChangelogTable` as follows:
```sql
SELECT * FROM spark_catalog.db.tbl.changes;
```

#### Pre/Post Update Images

The procedure computes the pre/post update images if configured. Pre/post update images are converted from a
pair of a delete row and an insert row. Identifier columns are used for determining whether an insert and a delete record
refer to the same row. If the two records share the same values for the identity columns they are considered to be before
and after states of the same row. You can either set identifier fields in the table schema or input them as the procedure parameters.

The following example shows pre/post update images computation with an identifier column(`id`), where a row deletion
and an insertion with the same `id` are treated as a single update operation. Specifically, suppose we have the following pair of rows:

| id  | name   | _change_type |
|-----|--------|--------------|
| 3   | Robert | DELETE       |
| 3   | Dan    | INSERT       |

In this case, the procedure marks the row before the update as an `UPDATE_BEFORE` image and the row after the update
as an `UPDATE_AFTER` image, resulting in the following pre/post update images:

| id  | name   | _change_type |
|-----|--------|--------------|
| 3   | Robert | UPDATE_BEFORE|
| 3   | Dan    | UPDATE_AFTER |
