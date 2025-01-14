[TOC]


# Syncing to Hive Metastore
This document walks through the steps to register a OneTable synced table on Hive Metastore (HMS).

## Pre-requisites
1. Source table(s) (Hudi/Delta/Iceberg) already written to your local storage or external storage locations like S3/GCS/ADLS.
   If you don't have the source table written in place already,
   you can follow the steps in [this]($Creating-Your-First-Interoperable-Table#create-dataset) tutorial to set it up.
2. A compute instance where you can run Apache Spark. This can be your local machine, docker,
   or a distributed system like Amazon EMR, Google Cloud's Dataproc, Azure HDInsight etc.
   This is a required step to register the table in HMS using a Spark client.
3. Clone the OneTable [repository](https://github.com/onetable-io/onetable) and create the
   `utilities-0.1.0-SNAPSHOT-bundled.jar` by following the steps on the [Installation page]($Installation)
4. This guide also assumes that you have configured the Hive Metastore locally or on EMR/Dataproc/HDInsight
   and is already running.

## Steps
### Running sync
Create `my_config.yaml` in the cloned OneTable directory.

> Hudi

```yaml
sourceFormat: DELTA|ICEBERG # choose only one
targetFormats:
  - HUDI
datasets:
  -
    tableBasePath: file:///path/to/source/data
    tableName: table_name
```

> Delta

```yaml
sourceFormat: HUDI|ICEBERG # choose only one
targetFormats:
  - DELTA
datasets:
  -
    tableBasePath: file:///path/to/source/data
    tableName: table_name
    partitionSpec: partitionpath:VALUE # you only need to specify partitionSpec for HUDI sourceFormat
```

> Iceberg

```yaml
sourceFormat: HUDI|DELTA # choose only one
targetFormats:
  - ICEBERG
datasets:
  -
    tableBasePath: file:///path/to/source/data
    tableName: table_name
    partitionSpec: partitionpath:VALUE # you only need to specify partitionSpec for HUDI sourceFormat
```

1. Replace with appropriate values for `sourceFormat`, `tableBasePath` and `tableName` fields.
2. Replace `file:///path/to/source/data` to appropriate source data path
   if you have your source table in S3/GCS/ADLS i.e.
    * S3 - `s3://path/to/source/data`
    * GCS - `gs://path/to/source/data` or
    * ADLS - `abfss://<container-name>@<storage-account-name>.dfs.core.windows.net/<path-to-data>`

From your terminal under the cloned OneTable directory, run the sync process using the below command.
```shell
java -jar utilities/target/utilities-0.1.0-SNAPSHOT-bundled.jar --datasetConfig my_config.yaml
```

> At this point, if you check your bucket path, you will be able to see `.hoodie` or `_delta_log` or `metadata`
> directory with relevant metadata files that helps query engines to interpret the data as a Hudi/Delta/Iceberg table.

### Register the target table in Hive Metastore
Now you need to register the OneTable synced target table in Hive Metastore.

> Hudi

A Hudi table can directly be synced to the Hive Metastore using Hive Sync Tool
and subsequently be queried by different query engines. For more information on the Hive Sync Tool, check
[Hudi Hive Metastore](https://hudi.apache.org/docs/syncing_metastore) docs.

```shell
cd $HUDI_HOME/hudi-sync/hudi-hive-sync

./run_sync_tool.sh  \
--jdbc-url <jdbc_url> \
--user <username> \
--pass <password> \
--partitioned-by <partition_field> \
--base-path <'/path/to/synced/hudi/table'> \
--database <database_name> \
--table <tableName>
```

> Replace `file:///path/to/source/data` to appropriate source data path
> if you have your source table in S3/GCS/ADLS i.e.
> * S3 - `s3://path/to/source/data`
> * GCS - `gs://path/to/source/data` or
> * ADLS - `abfss://<container-name>@<storage-account-name>.dfs.core.windows.net/<path-to-data>`


Now you will be able to query the created table directly as a Hudi table from the same `spark` session or
using query engines like `Presto` and/or `Trino`. Check out the guides for querying the OneTable synced tables on
[Presto]($Presto) or [Trino]($Trino) query engines for more information.

```sql
SELECT * FROM <database_name>.<table_name>;
```

> Delta

```shell
spark-sql --packages io.delta:delta-core_2.12:2.0.0 \
--conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" \
--conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog" \
--conf "spark.sql.catalogImplementation=hive"
```

In the `spark-sql` shell, you need to create a schema and table like below.

```sql
CREATE SCHEMA delta_db;

CREATE TABLE delta_db.<table_name> USING DELTA LOCATION '/path/to/synced/delta/table';
```

> Replace `file:///path/to/source/data` to appropriate source data path
> if you have your source table in S3/GCS/ADLS i.e.
> * S3 - `s3://path/to/source/data`
> * GCS - `gs://path/to/source/data` or
> * ADLS - `abfss://<container-name>@<storage-account-name>.dfs.core.windows.net/<path-to-data>`


Now you will be able to query the created table directly as a Delta table from the same `spark` session or
using query engines like `Presto` and/or `Trino`. Check out the guides for querying the OneTable synced tables on
[Presto]($Presto) or [Trino]($Trino) query engines for more information.

```sql
SELECT * FROM delta_db.<table_name>;
```

> Iceberg

```shell
spark-sql --packages org.apache.iceberg:iceberg-spark-runtime-3.2_2.12:1.2.1 \
--conf "spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions" \
--conf "spark.sql.catalog.spark_catalog=org.apache.iceberg.spark.SparkSessionCatalog" \
--conf "spark.sql.catalog.spark_catalog.type=hive" \
--conf "spark.sql.catalog.hive_prod=org.apache.iceberg.spark.SparkCatalog" \
--conf "spark.sql.catalog.hive_prod.type=hive"
```

In the `spark-sql` shell, you need to create a schema and table like below.

```sql
CREATE SCHEMA iceberg_db;

CALL hive_prod.system.register_table(
   table => 'hive_prod.iceberg_db.<table_name>',
   metadata_file => '/path/to/synced/iceberg/table/metadata/<VERSION>.metadata.json'
);

```

> Replace the dataset path while creating a dataframe to appropriate data path if you have your table
> in S3/GCS/ADLS i.e.
> * S3 - `s3://path/to/source/data`
> * GCS - `gs://path/to/source/data` or
> * ADLS - `abfss://<container-name>@<storage-account-name>.dfs.core.windows.net/<path-to-data>`

Now you will be able to query the created table directly as an Iceberg table from the same `spark` session or
using query engines like `Presto` and/or `Trino`. Check out the guides for querying the OneTable synced tables on
[Presto]($Presto) or [Trino]($Trino) query engines for more information.

```sql
SELECT * FROM iceberg_db.<table_name>;
```

## Conclusion
In this guide we saw how to,
1. sync a source table to create metadata for the desired target table formats using OneTable
2. catalog the data in the target table format in Hive Metastore
3. query the target table using Spark

