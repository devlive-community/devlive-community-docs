[TOC]

Below are properties set in `accumulo-client.properties` that configure [Accumulo clients]($Accumulo-Clients#connecting). All properties have been part of the API since 2.0.0 (unless otherwise specified):

| Property | Default value | Since | Description |
| --- | --- | --- | --- |
| instance.name | _empty_ | 2.0.0 | Name of Accumulo instance to connect to |
| instance.zookeepers | localhost:2181 | 2.0.0 | Zookeeper connection information for Accumulo instance |
| instance.zookeepers.timeout | 30s | 2.0.0 | Zookeeper session timeout |
| auth.type | password | 2.0.0 | Authentication method (i.e password, kerberos, PasswordToken, KerberosToken, etc) |
| auth.principal | _empty_ | 2.0.0 | Accumulo principal/username for chosen authentication method |
| auth.token | _empty_ | 2.0.0 | Authentication token (ex. mypassword, /path/to/keytab) |
| batch.writer.durability | default | 2.0.0 | The durability used to write to the write-ahead log. Legal values are: none, which skips the write-ahead log; log, which sends the data to the write-ahead log, but does nothing to make it durable; flush, which pushes data to the file system; and sync, which ensures the data is written to disk. Setting this property will change the durability for the BatchWriter session. A value of “default” will use the table’s durability setting. |
| batch.writer.latency.max | 120s | 2.0.0 | Max amount of time (in seconds) to hold data in memory before flushing it |
| batch.writer.memory.max | 50M | 2.0.0 | Max memory (in bytes) to batch before writing |
| batch.writer.threads.max | 3 | 2.0.0 | Maximum number of threads to use for writing data to tablet servers. |
| batch.writer.timeout.max | 0 | 2.0.0 | Max amount of time (in seconds) an unresponsive server will be re-tried. An exception is thrown when this timeout is exceeded. Set to zero for no timeout. |
| batch.scanner.num.query.threads | 3 | 2.0.0 | Number of concurrent query threads to spawn for querying |
| scanner.batch.size | 1000 | 2.0.0 | Number of key/value pairs that will be fetched at time from tablet server |
| ssl.enabled | false |   | Enable SSL for client RPC |
| ssl.keystore.password | _empty_ |   | Password used to encrypt keystore |
| ssl.keystore.path | _empty_ | 2.0.0 | Path to SSL keystore file |
| ssl.keystore.type | jks |   | Type of SSL keystore |
| ssl.truststore.password | _empty_ |   | Password used to encrypt truststore |
| ssl.truststore.path | _empty_ | 2.0.0 | Path to SSL truststore file |
| ssl.truststore.type | jks |   | Type of SSL truststore |
| ssl.use.jsse | false |   | Use JSSE system properties to configure SSL |
| sasl.enabled | false |   | Enable SASL for client RPC |
| sasl.kerberos.server.primary | accumulo |   | Kerberos principal/primary that Accumulo servers use to login |
| sasl.qop | auth |   | SASL quality of protection. Valid values are ‘auth’, ‘auth-int’, and ‘auth-conf’ |
