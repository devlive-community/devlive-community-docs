[TOC]

Trino just like Presto allows you to query table formats like Hudi, Delta and Iceberg tables using connectors.
Users do not need additional configurations to work with OneTable synced tables.

For more information and required configurations refer to:
* [Hudi Connector](https://trino.io/docs/current/connector/hudi.html)
* [Delta Lake Connector](https://trino.io/docs/current/connector/delta-lake.html)
* [Iceberg Connector](https://trino.io/docs/current/connector/iceberg.html)

For hands on experimentation, please follow [Creating your first interoperable table]($Creating-Your-First-Interoperable-Table#create-dataset)
to create OneTable synced tables followed by [Hive Metastore]($Hive-Metastore) to register the target table
in Hive Metastore. Once done, please follow the below high level steps:
1. Start the Trino server manually if you are working with a non-managed Trino service:
   from the trino-server directory run `./bin/launcher run`
2. From the directory where you have installed trino-cli: login to trino-cli by running `./trino-cli`
3. Start querying the table i.e. `SELECT * FROM catalog.schema.table;`.

> Hudi

> If you are following the example from [Hive Metastore]($Hive-Metastore), you can query the OneTable synced Hudi table
> from Trino using the below query.
>
> ```sql
> SELECT * FROM hudi.hudi_db.<table_name>;
> ```

> Delta

> If you are following the example from [Hive Metastore]($Hive-Metastore), you can query the OneTable synced Delta table
> from Trino using the below query.
>
> ```sql
> SELECT * FROM delta.delta_db.<table_name>;
> ```

> Iceberg

> If you are following the example from [Hive Metastore]($Hive-Metastore), you can query the OneTable synced Iceberg table
> from Trino using the below query.
>
> ```sql
> SELECT * FROM iceberg.iceberg_db.<table_name>;
> ```

