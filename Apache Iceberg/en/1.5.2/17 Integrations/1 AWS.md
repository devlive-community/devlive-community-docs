[TOC]

Iceberg provides integration with different AWS services through the `iceberg-aws` module.
This section describes how to use Iceberg with AWS.

## Enabling AWS Integration

The `iceberg-aws` module is bundled with Spark and Flink engine runtimes for all versions from `0.11.0` onwards.
However, the AWS clients are not bundled so that you can use the same client version as your application.
You will need to provide the AWS v2 SDK because that is what Iceberg depends on.
You can choose to use the [AWS SDK bundle](https://mvnrepository.com/artifact/software.amazon.awssdk/bundle),
or individual AWS client packages (Glue, S3, DynamoDB, KMS, STS) if you would like to have a minimal dependency footprint.

All the default AWS clients use the [Apache HTTP Client](https://mvnrepository.com/artifact/software.amazon.awssdk/apache-client)
for HTTP connection management.
This dependency is not part of the AWS SDK bundle and needs to be added separately.
To choose a different HTTP client library such as [URL Connection HTTP Client](https://mvnrepository.com/artifact/software.amazon.awssdk/url-connection-client),
see the section [client customization](#aws-client-customization) for more details.

All the AWS module features can be loaded through custom catalog properties,
you can go to the documentations of each engine to see how to load a custom catalog.
Here are some examples.

### Spark

For example, to use AWS features with Spark 3.4 (with scala 2.12) and AWS clients (which is packaged in the `iceberg-aws-bundle`), you can start the Spark SQL shell with:

```sh
# start Spark SQL client shell
spark-sql --packages org.apache.iceberg:iceberg-spark-runtime-3.4_2.12:{{ icebergVersion }},org.apache.iceberg:iceberg-aws-bundle:{{ icebergVersion }} \
    --conf spark.sql.defaultCatalog=my_catalog \
    --conf spark.sql.catalog.my_catalog=org.apache.iceberg.spark.SparkCatalog \
    --conf spark.sql.catalog.my_catalog.warehouse=s3://my-bucket/my/key/prefix \
    --conf spark.sql.catalog.my_catalog.type=glue \
    --conf spark.sql.catalog.my_catalog.io-impl=org.apache.iceberg.aws.s3.S3FileIO
```

As you can see, In the shell command, we use `--packages` to specify the additional `iceberg-aws-bundle` that contains all relevant AWS dependencies.

### Flink

To use AWS module with Flink, you can download the necessary dependencies and specify them when starting the Flink SQL client:

```sh
# download Iceberg dependency
ICEBERG_VERSION={{ icebergVersion }}
MAVEN_URL=https://repo1.maven.org/maven2
ICEBERG_MAVEN_URL=$MAVEN_URL/org/apache/iceberg

wget $ICEBERG_MAVEN_URL/iceberg-flink-runtime/$ICEBERG_VERSION/iceberg-flink-runtime-$ICEBERG_VERSION.jar

wget $ICEBERG_MAVEN_URL/iceberg-aws-bundle/$ICEBERG_VERSION/iceberg-aws-bundle-$ICEBERG_VERSION.jar

# start Flink SQL client shell
/path/to/bin/sql-client.sh embedded \
### Cross-Account and Cross-Region Access

It is a common use case for organizations to have a centralized AWS account for Glue metastore and S3 buckets, and use different AWS accounts and regions for different teams to access those resources.
In this case, a [cross-account IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use.html) is needed to access those centralized resources.
Iceberg provides an AWS client factory `AssumeRoleAwsClientFactory` to support this common use case.
This also serves as an example for users who would like to implement their own AWS client factory.

This client factory has the following configurable catalog properties:

| Property                          | Default                                  | Description                                            |
| --------------------------------- | ---------------------------------------- | ------------------------------------------------------ |
| client.assume-role.arn            | null, requires user input                | ARN of the role to assume, e.g. arn:aws:iam::123456789:role/myRoleToAssume  |
| client.assume-role.region         | null, requires user input                | All AWS clients except the STS client will use the given region instead of the default region chain  |
| client.assume-role.external-id    | null                                     | An optional [external ID](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)  |
| client.assume-role.timeout-sec    | 1 hour                                   | Timeout of each assume role session. At the end of the timeout, a new set of role session credentials will be fetched through an STS client.  |

By using this client factory, an STS client is initialized with the default credential and region to assume the specified role.
The Glue, S3 and DynamoDB clients are then initialized with the assume-role credential and region to access resources.
Here is an example to start Spark shell with this client factory:

```shell
spark-sql --packages org.apache.iceberg:iceberg-spark-runtime-3.4_2.12:{{ icebergVersion }},org.apache.iceberg:iceberg-aws-bundle:{{ icebergVersion }} \
    --conf spark.sql.catalog.my_catalog=org.apache.iceberg.spark.SparkCatalog \
    --conf spark.sql.catalog.my_catalog.warehouse=s3://my-bucket/my/key/prefix \    
    --conf spark.sql.catalog.my_catalog.type=glue \
    --conf spark.sql.catalog.my_catalog.client.factory=org.apache.iceberg.aws.AssumeRoleAwsClientFactory \
    --conf spark.sql.catalog.my_catalog.client.assume-role.arn=arn:aws:iam::123456789:role/myRoleToAssume \
    --conf spark.sql.catalog.my_catalog.client.assume-role.region=ap-northeast-1
```

### HTTP Client Configurations
AWS clients support two types of HTTP Client, [URL Connection HTTP Client](https://mvnrepository.com/artifact/software.amazon.awssdk/url-connection-client)
and [Apache HTTP Client](https://mvnrepository.com/artifact/software.amazon.awssdk/apache-client).
By default, AWS clients use **Apache** HTTP Client to communicate with the service.
This HTTP client supports various functionalities and customized settings, such as expect-continue handshake and TCP KeepAlive, at the cost of extra dependency and additional startup latency.
In contrast, URL Connection HTTP Client optimizes for minimum dependencies and startup latency but supports less functionality than other implementations.

For more details of configuration, see sections [URL Connection HTTP Client Configurations](#url-connection-http-client-configurations) and [Apache HTTP Client Configurations](#apache-http-client-configurations).

Configure the following property to set the type of HTTP client:

| Property         | Default | Description                                                                                                |
|------------------|---------|------------------------------------------------------------------------------------------------------------|
| http-client.type | apache  | Types of HTTP Client. <br/> `urlconnection`: URL Connection HTTP Client <br/> `apache`: Apache HTTP Client |

#### URL Connection HTTP Client Configurations

URL Connection HTTP Client has the following configurable properties:

| Property                                        | Default | Description                                                                                                                                                                                                      |
|-------------------------------------------------|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| http-client.urlconnection.socket-timeout-ms     | null    | An optional [socket timeout](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/urlconnection/UrlConnectionHttpClient.Builder.html#socketTimeout(java.time.Duration)) in milliseconds         |
| http-client.urlconnection.connection-timeout-ms | null    | An optional [connection timeout](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/urlconnection/UrlConnectionHttpClient.Builder.html#connectionTimeout(java.time.Duration)) in milliseconds |

Users can use catalog properties to override the defaults. For example, to configure the socket timeout for URL Connection HTTP Client when starting a spark shell, one can add:
```shell
--conf spark.sql.catalog.my_catalog.http-client.urlconnection.socket-timeout-ms=80
```

#### Apache HTTP Client Configurations

Apache HTTP Client has the following configurable properties:

| Property                                              | Default                   | Description                                                                                                                                                                                                                                 |
|-------------------------------------------------------|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| http-client.apache.socket-timeout-ms                  | null                      | An optional [socket timeout](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#socketTimeout(java.time.Duration)) in milliseconds |
| http-client.apache.connection-timeout-ms              | null                      | An optional [connection timeout](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#connectionTimeout(java.time.Duration)) in milliseconds |
| http-client.apache.connection-acquisition-timeout-ms  | null                      | An optional [connection acquisition timeout](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#connectionAcquisitionTimeout(java.time.Duration)) in milliseconds |
| http-client.apache.connection-max-idle-time-ms        | null                      | An optional [connection max idle timeout](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#connectionMaxIdleTime(java.time.Duration)) in milliseconds |
| http-client.apache.connection-time-to-live-ms         | null                      | An optional [connection time to live](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#connectionTimeToLive(java.time.Duration)) in milliseconds |
| http-client.apache.expect-continue-enabled            | null, disabled by default | An optional `true/false` setting that controls whether [expect continue](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#expectContinueEnabled(java.lang.Boolean)) is enabled |
| http-client.apache.max-connections                    | null                      | An optional [max connections](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#maxConnections(java.lang.Integer))  in integer       |
| http-client.apache.tcp-keep-alive-enabled             | null, disabled by default | An optional `true/false` setting that controls whether [tcp keep alive](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#tcpKeepAlive(java.lang.Boolean)) is enabled |
| http-client.apache.use-idle-connection-reaper-enabled | null, enabled by default  | An optional `true/false` setting that controls whether [use idle connection reaper](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/http/apache/ApacheHttpClient.Builder.html#useIdleConnectionReaper(java.lang.Boolean)) is used |

Users can use catalog properties to override the defaults. For example, to configure the max connections for Apache HTTP Client when starting a spark shell, one can add:
```shell
--conf spark.sql.catalog.my_catalog.http-client.apache.max-connections=5
```

## Run Iceberg on AWS

### Amazon Athena

[Amazon Athena](https://aws.amazon.com/athena/) provides a serverless query engine that could be used to perform read, write, update and optimization tasks against Iceberg tables.
More details could be found [here](https://docs.aws.amazon.com/athena/latest/ug/querying-iceberg.html).

### Amazon EMR

[Amazon EMR](https://aws.amazon.com/emr/) can provision clusters with [Spark](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark.html) (EMR 6 for Spark 3, EMR 5 for Spark 2),
[Hive](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive.html), [Flink](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-flink.html),
[Trino](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-presto.html) that can run Iceberg.

Starting with EMR version 6.5.0, EMR clusters can be configured to have the necessary Apache Iceberg dependencies installed without requiring bootstrap actions.
Please refer to the [official documentation](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-iceberg-use-cluster.html) on how to create a cluster with Iceberg installed.

For versions before 6.5.0, you can use a [bootstrap action](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html) similar to the following to pre-install all necessary dependencies:
```sh
#!/bin/bash

ICEBERG_VERSION={{ icebergVersion }}
MAVEN_URL=https://repo1.maven.org/maven2
ICEBERG_MAVEN_URL=$MAVEN_URL/org/apache/iceberg
# NOTE: this is just an example shared class path between Spark and Flink,
#  please choose a proper class path for production.
LIB_PATH=/usr/share/aws/aws-java-sdk/


ICEBERG_PACKAGES=(
  "iceberg-spark-runtime-3.3_2.12"
  "iceberg-flink-runtime"
  "iceberg-aws-bundle"
)

install_dependencies () {
  install_path=$1
  download_url=$2
  version=$3
  shift
  pkgs=("$@")
  for pkg in "${pkgs[@]}"; do
    sudo wget -P $install_path $download_url/$pkg/$version/$pkg-$version.jar
  done
}

install_dependencies $LIB_PATH $ICEBERG_MAVEN_URL $ICEBERG_VERSION "${ICEBERG_PACKAGES[@]}"
```

### AWS Glue

[AWS Glue](https://aws.amazon.com/glue/) provides a serverless data integration service
that could be used to perform read, write and update tasks against Iceberg tables.
More details could be found [here](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-programming-etl-format-iceberg.html).


### AWS EKS

[AWS Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/) can be used to start any Spark, Flink, Hive, Presto or Trino clusters to work with Iceberg.
Search the [Iceberg blogs](https://iceberg.apache.org/blogs/) page for tutorials around running Iceberg with Docker and Kubernetes.

### Amazon Kinesis

[Amazon Kinesis Data Analytics](https://aws.amazon.com/about-aws/whats-new/2019/11/you-can-now-run-fully-managed-apache-flink-applications-with-apache-kafka/) provides a platform
to run fully managed Apache Flink applications. You can include Iceberg in your application Jar and run it in the platform.
