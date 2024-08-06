[TOC]

Kyuubi provides several auxiliary SQL functions as supplement to
Flink's [Built-in Functions](https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/dev/table/functions/systemfunctions/)

|        Name         |                         Description                         | Return Type | Since |
|---------------------|-------------------------------------------------------------|-------------|-------|
| kyuubi_version      | Return the version of Kyuubi Server                         | string      | 1.8.0 |
| kyuubi_engine_name  | Return the application name for the associated query engine | string      | 1.8.0 |
| kyuubi_engine_id    | Return the application id for the associated query engine   | string      | 1.8.0 |
| kyuubi_system_user  | Return the system user name for the associated query engine | string      | 1.8.0 |
| kyuubi_session_user | Return the session username for the associated query engine | string      | 1.8.0 |

