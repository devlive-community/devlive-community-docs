[TOC]

Iceberg views support properties to configure view behavior. Below is an overview of currently available view properties.

|Property|Default|Description|
|---|---|---|
|write.metadata.compression-codec|gzip|Metadata compression codec: none or gzip|
|version.history.num-entries|10|Controls the number of versions to retain|
|replace.drop-dialect.allowed|false|Controls whether a SQL dialect is allowed to be dropped during a replace operation|

#### View behavior properties

|Property|Default|Description|
|---|---|---|
|commit.retry.num-retries|4|Number of times to retry a commit before failing|
|commit.retry.min-wait-ms|100|Minimum time in milliseconds to wait before retrying a commit|
|commit.retry.max-wait-ms|60000 (1 min)|Maximum time in milliseconds to wait before retrying a commit|
|commit.retry.total-timeout-ms|1800000 (30 min)|Total retry timeout period in milliseconds for a commit|
