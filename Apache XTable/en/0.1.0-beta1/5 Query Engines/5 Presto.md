[TOC]


Presto allows you to query table formats like Hudi, Delta and Iceberg using connectors. The same setup will
work for OneTable synced tables as well.

For more information and required configurations refer to:
* [Hudi Connector](https://prestodb.io/docs/current/connector/hudi.html)
* [Delta Lake](https://prestodb.io/docs/current/connector/deltalake.html)
* [Iceberg Connector](https://prestodb.io/docs/current/connector/iceberg.html)

> Delta Lake:
>
> Delta Lake supports [generated columns](https://docs.databricks.com/en/delta/generated-columns.html)
> which are a special type of column whose values are automatically generated based on a user-specified function
> over other columns in the Delta table. During sync, OneTable uses the same logic to generate partition columns wherever required.
> Currently, the generated columns from OneTable sync shows `NULL` when queried from Presto CLI.

For hands on experimentation, please follow [Creating your first interoperable table]($Installation) tutorial
to create OneTable synced tables followed by [Hive Metastore]($Hive-Metastore) tutorial to register the target table
in Hive Metastore. Once done, follow the below high level steps:
1. If you are working with a self-managed Presto service, from the presto-server directory run `./bin/launcher run`
2. From the directory where you have installed presto-cli: login to presto-cli by running `./presto-cli`
3. Start querying the table i.e. `SELECT * FROM catalog.schema.table;`.

> Hudi

> If you are following the example from [Hive Metastore]($Hive-Metastore), you can query the OneTable synced Hudi table
> from Presto using the below query.
>
> ```sql 
> SELECT * FROM hudi.hudi_db.<table_name>;
> ```

> Delta

> If you are following the example from [Hive Metastore]($Hive-Metastore), you can query the OneTable synced Delta table
> from Presto using the below query.
>
> ```sql 
> SELECT * FROM delta.delta_db.<table_name>;
> ```

> Iceberg

> If you are following the example from [Hive Metastore]($Hive-Metastore), you can query the OneTable synced Iceberg table
> from Presto using the below query.
>
> ```sql 
> SELECT * FROM iceberg.iceberg_db.<table_name>;
> ```

