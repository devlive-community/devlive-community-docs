[TOC]

## How to get the Kyuubi JDBC driver

Kyuubi Thrift API is fully compatible with HiveServer2, so technically, it allows to use any Hive JDBC driver to connect
Kyuubi Server. But it's recommended to use [Kyuubi Hive JDBC driver]($$Kyuubi-Hive-JDBC-Driver), which is forked from
Hive 3.1.x JDBC driver, aims to support some missing functionalities of the original Hive JDBC driver.

The driver is available from Maven Central:

```xml
<dependency>
    <groupId>org.apache.kyuubi</groupId>
    <artifactId>kyuubi-hive-jdbc-shaded</artifactId>
    <version>1.7.0</version>
</dependency>
```

## Connect to non-kerberized Kyuubi Server

The following java code connects directly to the Kyuubi Server by JDBC without using kerberos authentication.

```java
package org.apache.kyuubi.examples;
  
import java.sql.*;

public class KyuubiJDBC {

  private static String driverName = "org.apache.kyuubi.jdbc.KyuubiHiveDriver";
  private static String kyuubiJdbcUrl = "jdbc:kyuubi://localhost:10009/default;";

  public static void main(String[] args) throws SQLException {
    try (Connection conn = DriverManager.getConnection(kyuubiJdbcUrl)) {
      try (Statement stmt = conn.createStatement()) {
        try (ResultSet rs = stmt.executeQuery("show databases")) {
          while (rs.next()) {
            System.out.println(rs.getString(1));
          }
        }   
      }
    }
  }
}
```

## Connect to Kerberized Kyuubi Server

The following Java code uses a keytab file to login and connect to Kyuubi Server by JDBC.

```java
package org.apache.kyuubi.examples;

import java.sql.*;

public class KyuubiJDBCDemo {

  private static String driverName = "org.apache.kyuubi.jdbc.KyuubiHiveDriver";
  private static String kyuubiJdbcUrlTemplate = "jdbc:kyuubi://localhost:10009/default;" +
          "kyuubiClientPrincipal=%s;kyuubiClientKeytab=%s;kyuubiServerPrincipal=%s";

  public static void main(String[] args) throws SQLException {
    String clientPrincipal = args[0]; // Kerberos principal
    String clientKeytab = args[1];    // Keytab file location
    String serverPrincipal = args[2]; // Kerberos principal used by Kyuubi Server
    String kyuubiJdbcUrl = String.format(kyuubiJdbcUrlTemplate, clientPrincipal, clientKeytab, serverPrincipal);
    try (Connection conn = DriverManager.getConnection(kyuubiJdbcUrl)) {
      try (Statement stmt = conn.createStatement()) {
        try (ResultSet rs = stmt.executeQuery("show databases")) {
          while (rs.next()) {
            System.out.println(rs.getString(1));
          }
        }
      }
    }
  }
}
```


