[TOC]


# Syncing to Glue Data Catalog
This document walks through the steps to register a OneTable synced table in Glue Data Catalog on AWS.

## Pre-requisites
1. Source table(s) (Hudi/Delta/Iceberg) already written to Amazon S3.
   If you don't have the source table written in S3 already,
   you can follow the steps in [this]($Creating-Your-First-Interoperable-Table#create-dataset) tutorial to set it up
2. Setup access to interact with AWS APIs from the command line.
   If you haven’t installed AWSCLIv2, you do so by following the steps outlined in
   [AWS docs](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and
   also set up access credentials by following the steps
   [here](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html)
3. Clone the OneTable [repository](https://github.com/onetable-io/onetable) and create the
   `utilities-0.1.0-SNAPSHOT-bundled.jar` by following the steps on the [Installation page]($Installation)

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
    tableBasePath: s3://path/to/source/data
    tableName: table_name
```

> Delta

```yaml
sourceFormat: HUDI|ICEBERG # choose only one
targetFormats:
  - DELTA
datasets:
  -
    tableBasePath: s3://path/to/source/data
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
    tableBasePath: s3://path/to/source/data
    tableName: table_name
    partitionSpec: partitionpath:VALUE # you only need to specify partitionSpec for HUDI sourceFormat
```

> Replace with appropriate values for `sourceFormat`, `tableBasePath` and `tableName` fields.

From your terminal under the cloned onetable directory, run the sync process using the below command.

 ```shell
 java -jar utilities/target/utilities-0.1.0-SNAPSHOT-bundled.jar --datasetConfig my_config.yaml
 ```

> At this point, if you check your bucket path, you will be able to see the `.hoodie` or `_delta_log` or `metadata` directory
> with metadata files which contains the information that helps query engines interpret the data as the target table.

### Register the target table in Glue Data Catalog
From your terminal, create a glue database.

 ```shell
 aws glue create-database --database-input "{\"Name\":\"onetable_synced_db\"}"
 ```

From your terminal, create a glue crawler. Modify the `<yourAccountId>`, `<yourRoleName>`
and `<path/to/your/data>`, with appropriate values.

```shell
export accountId=<yourAccountId>
export roleName=<yourRoleName>
export s3DataPath=s3://<path/to/source/data>
```

> Hudi

```shell
aws glue create-crawler --name onetable_crawler --role arn:aws:iam::${accountId}:role/service-role/${roleName} --database onetable_synced_db --targets "{\"HudiTargets\":[{\"Paths\":[\"${s3DataPath}\"]}]}"
```

> Delta

```shell
aws glue create-crawler --name onetable_crawler --role arn:aws:iam::${accountId}:role/service-role/${roleName} --database onetable_synced_db --targets "{\"DeltaTargets\":[{\"Paths\":[\"${s3DataPath}\"]}]}"
```

> Iceberg

```shell
aws glue create-crawler --name onetable_crawler --role arn:aws:iam::${accountId}:role/service-role/${roleName} --database onetable_synced_db --targets "{\"IcebergTargets\":[{\"Paths\":[\"${s3DataPath}\"]}]}"
```

From your terminal, run the glue crawler.

```shell
 aws glue start-crawler --name onetable_crawler
```
Once the crawler succeeds, you’ll be able to query this Iceberg table from Athena,
EMR and/or Redshift query engines.

### Validating the results
After the crawler runs successfully, you can inspect the catalogued tables in Glue
and also query the table in Amazon Athena like below:

```sql
SELECT * FROM onetable_synced_db.<table_name>;
```

## Conclusion
In this guide we saw how to,
1. sync a source table to create metadata for the desired target table formats using OneTable
2. catalog the data in the target table format in Glue Data Catalog
3. query the target table using Amazon Athena

