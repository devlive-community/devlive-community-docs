[TOC]

> **New in version 1.4.0**: Kyuubi community maintains a forked Hive JDBC driver module and provides both shaded and non-shaded packages.

This packages aims to support some missing functionalities of the original Hive JDBC driver. For Kyuubi engines that support multiple catalogs, it provides meta APIs for better support. The behaviors of the original Hive JDBC driver have remained.

To access a Hive data warehouse or new Lakehouse formats, such as Apache Iceberg/Hudi, Delta Lake using the Kyuubi JDBC driver for Apache kyuubi, you need to configure the following:

*   The list of driver library files - [Referencing the JDBC Driver Libraries](#referencing-libraries).
*   The Driver or DataSource class - [Registering the Driver Class](#registering-class).
*   The connection URL for the driver - [Building the Connection URL](#building-url)

Referencing the JDBC Driver Libraries
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Before you use the jdbc driver for Apache Kyuubi, the JDBC application or Java code that you are using to connect to your data must be able to access the driver JAR files.

### Using the Driver in Java Code

In the code, specify the artifact kyuubi-hive-jdbc-shaded from [Maven Central](https://mvnrepository.com/artifact/org.apache.kyuubi/kyuubi-hive-jdbc-shaded) according to the build tool you use.

#### Maven

```xml
<dependency>
    <groupId>org.apache.kyuubi</groupId>
    <artifactId>kyuubi-hive-jdbc-shaded</artifactId>
    <version>1.9.1</version>
</dependency>
```

#### sbt

```shell
libraryDependencies += "org.apache.kyuubi" % "kyuubi-hive-jdbc-shaded" % "1.9.1"
```

#### Gradle

```shell
implementation group: 'org.apache.kyuubi', name: 'kyuubi-hive-jdbc-shaded', version: '1.9.1'
```

### Using the Driver in a JDBC Application

For [JDBC Applications]($Business-Intelligence-Tools-And-SQL-IDEs), such as BI tools, SQL IDEs, please check the specific guide for detailed information.

> Is your favorite tool missing? [Report an feature request](https://kyuubi.apache.org/issue_tracking.html) or help us document it.

Registering the Driver Class
---------------------------------------------------------------------------------------------------------------------------------------------------------

Before connecting to your data, you must register the JDBC Driver class for your application.

*   org.apache.kyuubi.jdbc.KyuubiHiveDriver
*   org.apache.kyuubi.jdbc.KyuubiDriver (Deprecated)

The following sample code shows how to use the [java.sql.DriverManager](https://docs.oracle.com/javase/8/docs/api/java/sql/DriverManager.html) class to establish a connection for JDBC:

```java
private static Connection newKyuubiConnection() throws Exception {
  Connection connection = DriverManager.getConnection(CONNECTION_URL);
  return connection;
}
```

Building the Connection URL
-------------------------------------------------------------------------------------------------------------------------------------------------------

### Basic Connection URL format

Use the connection URL to supply connection information to the kyuubi server or cluster that you are accessing. The following is the format of the connection URL for the Kyuubi Hive JDBC Driver

```shell
jdbc:subprotocol://host:port[/catalog]/[schema];<clientProperties;><[#|?]sessionProperties>
```

*   subprotocol: kyuubi or hive2
*   host: DNS or IP address of the kyuubi server
*   port: The number of the TCP port that the server uses to listen for client requests
*   catalog: Optional catalog name to set the current catalog to run the query against.
*   schema: Optional database name to set the current database to run the query against, use default if absent.
*   clientProperties: Optional semicolon(;) separated key=value parameters identified and affect the client behavior locally. e.g., user=foo;password=bar.
*   sessionProperties: Optional semicolon(;) separated key=value parameters used to configure the session, operation or background engines. For instance, kyuubi.engine.share.level=CONNECTION determines the background engine instance is used only by the current connection. spark.ui.enabled=false disables the Spark UI of the engine.

Important

> *   The sessionProperties MUST come after a leading number sign(#) or question mark (?).
> * Properties are case-sensitive
> *   Do not duplicate properties in the connection URL


### Connection URL over HTTP

> New in version 1.6.0.

```shell
jdbc:subprotocol://host:port/schema;transportMode=http;httpPath=<http_endpoint>
```

*   http_endpoint is the corresponding HTTP endpoint configured by `kyuubi.frontend.thrift.http.path` at the server side.

### Connection URL over Service Discovery

```shell
jdbc:subprotocol://<zookeeper quorum>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=kyuubi
```

*   zookeeper quorum is the corresponding zookeeper cluster configured by `kyuubi.ha.addresses` at the server side.
*   zooKeeperNamespace is the corresponding namespace configured by `kyuubi.ha.namespace` at the server side.

### HiveServer2 Compatibility

> New in version 1.8.0.

JDBC Drivers need to negotiate a protocol version with Kyuubi Server/HiveServer2 when connecting.

Kyuubi Hive JDBC Driver offers protocol version v10 (`clientProtocolVersion=9`, supported since Hive 2.3.0) to server by default.

If you need to connect to HiveServer2 before 2.3.0, please set client property clientProtocolVersion to a lower number.

```shell
jdbc:subprotocol://host:port[/catalog]/[schema];clientProtocolVersion=9;
```

> All supported protocol versions and corresponding Hive versions can be found in [TProtocolVersion.java](https://github.com/apache/hive/blob/master/service-rpc/src/gen/thrift/gen-javabean/org/apache/hive/service/rpc/thrift/TProtocolVersion.java) and its git commits.

Kerberos Authentication
-----------------------------------------------------------------------------------------------------------------------------------------------

Since 1.6.0, Kyuubi JDBC driver implements the Kerberos authentication based on JAAS framework instead of [Hadoop UserGroupInformation](https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/security/UserGroupInformation.html), which means it does not forcibly rely on Hadoop dependencies to connect a kerberized Kyuubi Server.

Kyuubi JDBC driver supports different approaches to connect a kerberized Kyuubi Server. First of all, please follow the [krb5.conf instruction](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html) to setup `krb5.conf` properly.

### Authentication by Principal and Keytab

> New in version 1.6.0.

> It’s the simplest way w/ minimal setup requirements for Kerberos authentication.

It’s straightforward to use principal and keytab for Kerberos authentication, just simply configure them in the JDBC URL.

```shell
jdbc:kyuubi://host:port/schema;kyuubiClientPrincipal=<clientPrincipal>;kyuubiClientKeytab=<clientKeytab>;kyuubiServerPrincipal=<serverPrincipal>
```

*   kyuubiClientPrincipal: Kerberos `principal` for client authentication
*   kyuubiClientKeytab: path of Kerberos `keytab` file for client authentication
*   kyuubiClientTicketCache: path of Kerberos `ticketCache` file for client authentication, available since 1.8.0.
*   kyuubiServerPrincipal: Kerberos `principal` configured by kyuubi.kinit.principal at the server side. `kyuubiServerPrincipal` is available as an alias of `principal` since 1.7.0, use `principal` for previous versions.

### Authentication by Principal and TGT Cache

Another typical usage of Kerberos authentication is using kinit to generate the TGT cache first, then the application does Kerberos authentication through the TGT cache.

```shell
jdbc:kyuubi://host:port/schema;kyuubiServerPrincipal=<serverPrincipal>
```

### Authentication by [Hadoop UserGroupInformation](https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/security/UserGroupInformation.html) `doAs` (programing only)

> This approach allows project which already uses [Hadoop UserGroupInformation](https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/security/UserGroupInformation.html) for Kerberos authentication to easily connect the kerberized Kyuubi Server. This approach does not work between \[1.6.0, 1.7.0\], and got fixed in 1.7.1.

```java
String jdbcUrl = "jdbc:kyuubi://host:port/schema;kyuubiServerPrincipal=<serverPrincipal>"
UserGroupInformation ugi = UserGroupInformation.loginUserFromKeytab(clientPrincipal, clientKeytab);
ugi.doAs((PrivilegedExceptionAction<String>) () -> {
  Connection conn = DriverManager.getConnection(jdbcUrl);
  ...
});
```

### Authentication by Subject (programing only)

```java
String jdbcUrl = "jdbc:kyuubi://host:port/schema;kyuubiServerPrincipal=<serverPrincipal>;kerberosAuthType=fromSubject"
Subject kerberizedSubject = ...;
Subject.doAs(kerberizedSubject, (PrivilegedExceptionAction<String>) () -> {
  Connection conn = DriverManager.getConnection(jdbcUrl);
  ...
});
```
