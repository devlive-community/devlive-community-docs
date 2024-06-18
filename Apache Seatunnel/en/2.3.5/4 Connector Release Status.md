[TOC]

SeaTunnel uses a grading system for connectors to help you understand what to expect from a connector:

|                      |                                                                                                      Alpha                                                                                                       |                                                                                                                    Beta                                                                                                                    |                                                                                           General Availability (GA)                                                                                            |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Expectations         | An alpha connector signifies a connector under development and helps SeaTunnel gather early feedback and issues reported by early adopters. We strongly discourage using alpha releases for production use cases | A beta connector is considered stable and reliable with no backwards incompatible changes but has not been validated by a broader group of users. We expect to find and fix a few issues and bugs in the release before it’s ready for GA. | A generally available connector has been deemed ready for use in a production environment and is officially supported by SeaTunnel. Its documentation is considered sufficient to support widespread adoption. |
|                      |                                                                                                                                                                                                                  |                                                                                                                                                                                                                                            |                                                                                                                                                                                                                |
| Production Readiness | No                                                                                                                                                                                                               | Yes                                                                                                                                                                                                                                        | Yes                                                                                                                                                                                                            |

## Connector V2 Health

|                       Connector Name                        |  Type  | Status | Support Version |
|-------------------------------------------------------------|--------|--------|-----------------|
| [AmazonDynamoDB]($SK-AmazonDynamoDB)       | Sink   | Beta   | 2.3.0           |
| [AmazonDynamoDB]($AmazonDynamoDB)     | Source | Beta   | 2.3.0           |
| [Asset]($SK-Assert)                        | Sink   | Beta   | 2.2.0-beta      |
| [Cassandra]($SK-Cassandra)                 | Sink   | Beta   | 2.3.0           |
| [Cassandra]($Cassandra)               | Source | Beta   | 2.3.0           |
| [ClickHouse]($Clickhouse)             | Source | GA     | 2.2.0-beta      |
| [ClickHouse]($SK-Clickhouse)               | Sink   | GA     | 2.2.0-beta      |
| [ClickHouseFile]($SK-ClickhouseFile)       | Sink   | GA     | 2.2.0-beta      |
| [Console]($SK-Console)                     | Sink   | GA     | 2.2.0-beta      |
| [DataHub]($SK-Datahub)                     | Sink   | Alpha  | 2.2.0-beta      |
| [Doris]($SK-Doris)                         | Sink   | Beta   | 2.3.0           |
| [DingTalk]($SK-DingTalk)                   | Sink   | Alpha  | 2.2.0-beta      |
| [Elasticsearch]($SK-Elasticsearch)         | Sink   | GA     | 2.2.0-beta      |
| [Email]($SK-Email)                         | Sink   | Alpha  | 2.2.0-beta      |
| [Enterprise WeChat]($SK-Enterprise-WeChat) | Sink   | Alpha  | 2.2.0-beta      |
| [FeiShu]($SK-Feishu)                       | Sink   | Alpha  | 2.2.0-beta      |
| [Fake]($FakeSource)                   | Source | GA     | 2.2.0-beta      |
| [FtpFile]($SK-FtpFile)                     | Sink   | Beta   | 2.2.0-beta      |
| [Greenplum]($SK-Greenplum)                 | Sink   | Beta   | 2.2.0-beta      |
| [Greenplum]($Greenplum)               | Source | Beta   | 2.2.0-beta      |
| [HdfsFile]($SK-HdfsFile)                   | Sink   | GA     | 2.2.0-beta      |
| [HdfsFile]($HdfsFile)                 | Source | GA     | 2.2.0-beta      |
| [Hive]($SK-Hive)                           | Sink   | GA     | 2.2.0-beta      |
| [Hive]($Hive)                         | Source | GA     | 2.2.0-beta      |
| [Http]($SK-Http)                           | Sink   | Beta   | 2.2.0-beta      |
| [Http]($Http)                         | Source | Beta   | 2.2.0-beta      |
| [Hudi]($Hudi)                         | Source | Beta   | 2.2.0-beta      |
| [Iceberg]($Iceberg)                   | Source | Beta   | 2.2.0-beta      |
| [InfluxDB]($SK-InfluxDB)                   | Sink   | Beta   | 2.3.0           |
| [InfluxDB]($InfluxDB)                 | Source | Beta   | 2.3.0-beta      |
| [IoTDB]($IoTDB)                       | Source | GA     | 2.2.0-beta      |
| [IoTDB]($SK-IoTDB)                         | Sink   | GA     | 2.2.0-beta      |
| [Jdbc]($Jdbc)                         | Source | GA     | 2.2.0-beta      |
| [Jdbc]($SK-Jdbc)                           | Sink   | GA     | 2.2.0-beta      |
| [Kafka]($kafka)                       | Source | GA     | 2.3.0           |
| [Kafka]($SK-Kafka)                         | Sink   | GA     | 2.2.0-beta      |
| [Kudu]($Kudu)                         | Source | Beta   | 2.2.0-beta      |
| [Kudu]($SK-Kudu)                           | Sink   | Beta   | 2.2.0-beta      |
| [Lemlist]($Lemlist)                   | Source | Beta   | 2.3.0           |
| [LocalFile]($SK-LocalFile)                 | Sink   | GA     | 2.2.0-beta      |
| [LocalFile]($LocalFile)               | Source | GA     | 2.2.0-beta      |
| [Maxcompute]($Maxcompute)             | Source | Alpha  | 2.3.0           |
| [Maxcompute]($SK-Maxcompute)               | Sink   | Alpha  | 2.3.0           |
| [MongoDB]($MongoDB)                   | Source | Beta   | 2.2.0-beta      |
| [MongoDB]($SK-MongoDB)                     | Sink   | Beta   | 2.2.0-beta      |
| [MyHours]($MyHours)                   | Source | Alpha  | 2.2.0-beta      |
| [MySqlCDC]($MySQL-CDC)                | Source | GA     | 2.3.0           |
| [Neo4j]($SK-Neo4j)                         | Sink   | Beta   | 2.2.0-beta      |
| [Notion]($Notion)                     | Source | Alpha  | 2.3.0           |
| [OneSignal]($OneSignal)               | Source | Beta   | 2.3.0           |
| [OpenMldb]($OpenMldb)                 | Source | Beta   | 2.3.0           |
| [OssFile]($SK-OssFile)                     | Sink   | Beta   | 2.2.0-beta      |
| [OssFile]($OssFile)                   | Source | Beta   | 2.2.0-beta      |
| [Phoenix]($SK-Phoenix)                     | Sink   | Beta   | 2.2.0-beta      |
| [Phoenix]($Phoenix)                   | Source | Beta   | 2.2.0-beta      |
| [Pulsar]($Pulsar)                     | Source | Beta   | 2.2.0-beta      |
| [RabbitMQ]($SK-Rabbitmq)                   | Sink   | Beta   | 2.3.0           |
| [RabbitMQ]($Rabbitmq)                 | Source | Beta   | 2.3.0           |
| [Redis]($SK-Redis)                         | Sink   | Beta   | 2.2.0-beta      |
| [Redis]($Redis)                       | Source | Beta   | 2.2.0-beta      |
| [S3Redshift]($SK-S3-Redshift)              | Sink   | GA     | 2.3.0-beta      |
| [S3File]($S3File)                     | Source | GA     | 2.3.0-beta      |
| [S3File]($SK-S3File)                       | Sink   | GA     | 2.3.0-beta      |
| [Sentry]($SK-Sentry)                       | Sink   | Alpha  | 2.2.0-beta      |
| [SFtpFile]($SK-SftpFile)                   | Sink   | Beta   | 2.3.0           |
| [SFtpFile]($SftpFile)                 | Source | Beta   | 2.3.0           |
| [Slack]($SK-Slack)                         | Sink   | Beta   | 2.3.0           |
| [Socket]($SK-Socket)                       | Sink   | Beta   | 2.2.0-beta      |
| [Socket]($Socket)                     | Source | Beta   | 2.2.0-beta      |
| [StarRocks]($SK-StarRocks)                 | Sink   | Alpha  | 2.3.0           |
| [Tablestore]($SK-Tablestore)               | Sink   | Alpha  | 2.3.0           |


