[TOC]

Kyuubi provides several auxiliary SQL functions as supplement to Spark's [Built-in Functions](https://spark.apache.org/docs/latest/api/sql/index.html#built-in-functions)

|      Name      |                            Description                            | Return Type | Since |
|----------------|-------------------------------------------------------------------|-------------|-------|
| kyuubi_version | Return the version of Kyuubi Server                               | string      | 1.3.0 |
| engine_name    | Return the spark application name for the associated query engine | string      | 1.3.0 |
| engine_id      | Return the spark application id for the associated query engine   | string      | 1.4.0 |
| system_user    | Return the system user name for the associated query engine       | string      | 1.3.0 |
| session_user   | Return the session username for the associated query engine       | string      | 1.4.0 |
| engine_url     | Return the engine url for the associated query engine             | string      | 1.8.0 |

