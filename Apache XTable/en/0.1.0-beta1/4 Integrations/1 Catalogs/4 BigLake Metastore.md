[TOC]

This document walks through the steps to register a OneTable synced Iceberg table in BigLake Metastore on GCP.

## Pre-requisites
1. Source (Hudi/Delta) table(s) already written to Google Cloud Storage.
   If you don't have the source table written in GCS,
   you can follow the steps in [this]($Creating-Your-First-Interoperable-Table#create-dataset) tutorial to set it up.
2. To ensure that the BigLake API's caller (your service account used by OneTable) has the
   necessary permissions to create a BigLake table, ask your administrator to grant [BigLake Admin](https://cloud.google.com/iam/docs/understanding-roles#biglake.admin) (roles/bigquery.admin)
   access to the service account.
3. To ensure that the Storage Account API's caller (your service account used by OneTable) has the
   necessary permissions to write log/metadata files in GCS, ask your administrator to grant [Storage Object User](https://cloud.google.com/storage/docs/access-control/iam-roles) (roles/storage.objectUser)
   access to the service account.
4. If you're running OneTable outside GCP, you need to provide the machine access to interact with BigLake and GCS.
   To do so, store the permissions key for your service account in your machine using
   ```shell
   export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service_account_key.json
   ```
5. Clone the OneTable [repository](https://github.com/onetable-io/onetable) and create the
   `utilities-0.1.0-SNAPSHOT-bundled.jar` by following the steps on the [Installation page]($Installation)
6. Download the [BigLake Iceberg JAR](gs://spark-lib/biglake/biglake-catalog-iceberg1.2.0-0.1.0-with-dependencies.jar) locally.
   OneTable requires the JAR to be present in the classpath.

## Steps
> Currently BigLake Metastore is only accessible through Google's
> [BigLake Rest APIs](https://cloud.google.com/bigquery/docs/reference/biglake/rest), and as such
> OneTable requires you to setup the below items prior to running sync on your source dataset.
>    * BigLake Catalog
>    * BigLake Database

### Create BigLake Catalog
Use the `Try this method` on Google's REST reference docs for
[`projects.locations.catalogs.create`](https://cloud.google.com/bigquery/docs/reference/biglake/rest/v1/projects.locations.catalogs/create)
method to create a catalog.

In this tutorial we'll use `us-west1` region.
```rest
projects/<yourProjectName>/locations/us-west1/catalogs
```
```rest
onetable
```

### Create BigLake Database
Use the `Try this method` on Google's REST reference docs for
[`projects.locations.catalogs.databases.create`](https://cloud.google.com/bigquery/docs/reference/biglake/rest/v1/projects.locations.catalogs/create)
method to create a database.
```rest
projects/<yourProjectName>/locations/us-west1/catalogs/onetable/databases
```
```rest
onetable_synced_db
```

### Running sync

> Hudi

```yaml
sourceFormat: HUDI
targetFormats:
  - ICEBERG
datasets:
  -
    tableBasePath: gs://path/to/source/data
    tableName: table_name
    namespace: database_name
```

> Delta

```yaml
sourceFormat: DELTA
targetFormats:
  - ICEBERG
datasets:
  -
    tableBasePath: gs://path/to/source/data
    tableName: table_name
    namespace: onetable_synced_db
```

The catalog information can be specified in a yaml file and passed in with the `--icebergCatalogConfig` option.
An example `catalog.yaml` file to sync with BigLake Metastore:

```yaml
catalogImpl: org.apache.iceberg.gcp.biglake.BigLakeCatalog
catalogName: onetable
catalogOptions:
  gcp_project: <yourProjectName>
  gcp_location: us-west1
  warehouse: gs://path/to/warehouse
```

From your terminal under the cloned OneTable directory, run the sync process using the below command.

```shell
java -cp utilities/target/utilities-0.1.0-SNAPSHOT-bundled.jar:/path/to/downloaded/biglake-catalog-iceberg1.2.0-0.1.0-with-dependencies.jar io.onetable.utilities.RunSync  --datasetConfig my_config.yaml --icebergCatalogConfig catalog.yaml
```

> At this point, if you check your bucket path, you will be able to see the `metadata` directory
> with metadata files which contains the information that helps query engines
> to interpret the data as an Iceberg table.

### Validating the results
Once the sync succeeds, OneTable would have written the table directly to BigLake Metastore.
We can use `Try this method` option on Google's REST reference docs for
[`projects.locations.catalogs.databases.tables.get`](https://cloud.google.com/bigquery/docs/reference/biglake/rest/v1/projects.locations.catalogs.databases.tables/get)
method to view the created table.
```rest md title="name"
projects/<yourProjectName>/locations/us-west1/catalogs/onetable/databases/onetable_synced_db/tables/table_name
```

## Conclusion
In this guide we saw how to,
1. sync a source table to create Iceberg metadata with OneTable
2. catalog the data as an Iceberg table in BigLake Metastore
3. validate the table creation using `projects.locations.catalogs.databases.tables.get` method

