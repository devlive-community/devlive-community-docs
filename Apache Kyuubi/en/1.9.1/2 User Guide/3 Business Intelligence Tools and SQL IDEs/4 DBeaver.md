[TOC]

What is DBeaver
-------------------------------------------------------------------------------------------------------------------------------

![Image 3: https://raw.githubusercontent.com/wiki/dbeaver/dbeaver/images/dbeaver-icon-64x64.png](https://raw.githubusercontent.com/wiki/dbeaver/dbeaver/images/dbeaver-icon-64x64.png)[DBeaver](https://dbeaver.io/) is a free multi-platform database tool for developers, database administrators, analysts, and all people who need to work with databases. Supports all popular databases as well as kyuubi JDBC.

> See also
> 
> DBeaver Wiki

Installation
-------------------------------------------------------------------------------------------------------------------------

Please go to [Download DBeaver](https://dbeaver.io/download/) page to get and install an appropriate release version for yourself.

New in version 22.1.0(dbeaver): DBeaver officially supports apache kyuubi JDBC driver since 06 Jun 2022 via [PR 16567](https://github.com/dbeaver/dbeaver/issues/16567).

Using DBeaver with Kyuubi
---------------------------------------------------------------------------------------------------------------------------------------------------

If you have successfully installed dbeaver, just hit the button to launch it.

### New Connection

Firstly, we need to create a database connection against a live kyuubi server. You are able to find the kyuubi jdbc driver since dbeaver 22.1.0, as shown in the following figure.

![Image 4: ../../_images/new_database_connection.png](https://kyuubi.readthedocs.io/en/v1.9.1/_images/new_database_connection.png)

> We can also choose Apache Hive or Apache Spark to set up a driver for Kyuubi, because they are compatible with the same client.

### Configure Connection

Secondly, we configure the JDBC connection settings to format an underlying kyuubi JDBC connection URL string.

#### Basic Connection Settings

The basic connection setting contains a minimal set of items you need to talk with kyuubi server,

*   Host - hostname or IP address that the kyuubi server bound with, default: localhost.
*   Port - port that the kyuubi server listening to, default: 10009.
*   Database/Schema - database or schema to use, default: default.
*   Authentication - identity information, such as user/password, based on the server authentication mechanism.

#### Session Configurations

Session configuration list is an optional part of kyuubi JDBC URLs, which are very helpful to override some configurations of the kyuubi server at session scope. The setup page of dbeaver does not contain any text box for such behavior. However, we can append the semicolon-separated configuration pairs to the Database/Schema filed leading with a number sign(#). Though it’s a bit weird, but it works.

![Image 5: ../../_images/configure_database_connection.png](https://kyuubi.readthedocs.io/en/v1.9.1/_images/configure_database_connection.png)As an example, shown in the picture above, the engine uses 2 gigabytes memory for the driver process of kyuubi engine and will be terminated after idle for 30 seconds.

#### Connecting in HA mode

Kyuubi supports HA by service discovery over Apache Zookeeper cluster.

![Image 6: ../../_images/configure_database_connection_ha.png](https://kyuubi.readthedocs.io/en/v1.9.1/_images/configure_database_connection_ha.png)As an example, shown in the above picture, the Host and Port fields can be used to concat the comma separated zookeeper peers, while the serviceDiscoveryMode and zooKeeperNamespace are appended to the Database/Schema field.

### Test Connection

It is not necessary but recommended to click Test Connection to verify the connection is set correctly. If something wrong happens at the client side or server side, we can debug ahead with the error message.

### SQL Operations

Now, we can use the SQL editor to write queries to interact with Kyuubi server through the connection.

```sql
DESC NAMESPACE DEFAULT;
```

```sql
CREATE TABLE spark_catalog.`default`.SRC(KEY INT, VALUE STRING) USING PARQUET;
INSERT INTO TABLE spark_catalog.`default`.SRC VALUES (11215016, 'Kent Yao');
```

```sql
SELECT KEY % 10 AS ID, SUBSTRING(VALUE, 1, 4) AS NAME FROM spark_catalog.`default`.SRC;
```

![Image 7: ../../_images/metadata.png](https://kyuubi.readthedocs.io/en/v1.9.1/_images/metadata.png)

```sql
DROP TABLE spark_catalog.`default`.SRC;
```

Client Authentication
-------------------------------------------------------------------------------------------------------------------------------------------

For kerberized kyuubi clusters, please refer to [Kerberos Authentication](https://kyuubi.readthedocs.io/en/v1.9.1/client/advanced/kerberized_kyuubi.html#bi-tools) for more information.
