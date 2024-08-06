[TOC]

This page covers how to start with kyuubi quickly on you laptop in about 3~5 minutes.

Requirements
-------------------------------------------------------------------------------------------------------------------------

For quick start deployment, we need to prepare the following stuffs:

*   A **client** that connects and submits queries to the server. Here, we use the kyuubi beeline for demonstration.
*   A **server** that serves clients and manages engines.
*   An **engine** that is used to instantiate query execution environments. Here we use Spark for demonstration.

These essential components are JVM-based applications. So, the JRE needs to be pre-installed and the `JAVA_HOME` is correctly set to each component.

The other internal or external parts listed in the above sheet can be used individually or all together. For example, you can use Kyuubi, Spark and Flink to build a streaming data warehouse. And then, you can use Zookeeper to enable the load balancing for high availability. The data could be stored in Hive, Apache Iceberg, or other DBMSs.

In what follows, we will only use Kyuubi and Spark.

Installation
-------------------------------------------------------------------------------------------------------------------------

> This following instructions are based on binary releases. If you start with source releases, please refer to the page for [building kyuubi](https://kyuubi.readthedocs.io/en/v1.9.1/develop_tools/distribution.html).

### Install Kyuubi

The official releases, binary- and source-, are archived on the [download page](https://kyuubi.apache.org/releases.html). Please download the most recent stable release to start.

To install Kyuubi, you need to unpack the tarball. For example,

```java
$ tar zxf apache-kyuubi-1.9.1-bin.tgz
```

```java
├── LICENSE
├── NOTICE
├── RELEASE
├── beeline-jars
├── bin
├── charts
│   └── kyuubi
├── conf
|   ├── kyuubi-defaults.conf.template
│   ├── kyuubi-env.sh.template
│   └── log4j2.xml.template
├── db-scripts
│   ├── mysql
│   ├── postgresql
│   └── sqlite
├── docker
│   ├── Dockerfile
│   └── playground
├── externals
│  └── engines
├── jars
├── licenses
├── logs
├── pid
├── web-ui
└── work
```

From top to bottom are:

*   LICENSE: the APACHE [LICENSE](https://www.apache.org/licenses/LICENSE-2.0), VERSION 2.0 we claim to obey.
*   RELEASE: the build information of this package.
*   NOTICE: the notice made by Apache Kyuubi Community about its project and dependencies.
*   bin: the entry of the Kyuubi server with kyuubi as the startup script.
*   conf: all the defaults used by Kyuubi Server itself or creating a session with engines.
*   externals - engines: contains all kinds of SQL engines that we support
*   licenses: a bunch of licenses included.
*   jars: packages needed by the Kyuubi server.
*   logs: where the logs of the Kyuubi server locates.
*   pid: stores the PID file of the Kyuubi server instance.
*   work: the root of the working directories of all the forked sub-processes, a.k.a. SQL engines.

### Install Spark

The official releases, binary- and source-, are archived on the [spark download page](https://spark.apache.org/downloads.html). Please download the most recent stable release to start.

> Currently, Kyuubi is compiled and pre-built against Spark 3 and Scala 2.12 You will probably meet runtime exceptions if you use Spark 2 or Spark with unsupported Scala versions.

To install Spark, you need to unpack the tarball. For example,

```java
$ tar zxf spark-3.4.2-bin-hadoop3.tgz
```

### Configuration

The kyuubi-env.sh file is used to set system environment variables to the kyuubi server process and engine processes it creates.

The kyuubi-defaults.conf file is used to set system properties to the kyuubi server process and engine processes it creates.

Each file has a template lays in conf directory for your information. The following are examples of the parameters necessary for a quick start with Spark.

*   **JAVA\_HOME**

```java
$ echo 'export JAVA\_HOME=/path/to/java' >> conf/kyuubi-env.sh
```

*   **SPARK\_HOME**

```java
$ echo 'export SPARK\_HOME=/path/to/spark' >> conf/kyuubi-env.sh
```

Start Kyuubi
-------------------------------------------------------------------------------------------------------------------------

If script above runs successfully, it will store the PID of the server instance into `pid/kyuubi-<username>-org.apache.kyuubi.server.KyuubiServer.pid`. And you are able to get the JDBC connection URL from the log file - `logs/kyuubi-<username>-org.apache.kyuubi.server.KyuubiServer-<hostname>.out`.

For example,

> Starting and exposing JDBC connection at: jdbc:hive2://localhost:10009/

If something goes wrong, you shall be able to find some clues in the log file too.

> Alternatively, it can run in the foreground, with the logs and other output written to stdout/stderr. Both streams should be captured if using a supervision system like supervisord.
> 
> `bin/kyuubi run`

Operate Clients
-------------------------------------------------------------------------------------------------------------------------------

Kyuubi delivers a beeline client, enabling a similar experience to Apache Hive use cases.

### Open Connections

Replace the host and port with the actual ones you’ve got in the step of server startup for the following JDBC URL. The case below open a session for user named apache.

```java
$ bin/beeline -u 'jdbc:hive2://localhost:10009/' -n apache
```

> Use –help to display the usage guide for the beeline tool.
> 
> `bin/beeline --help`

### Execute Statements

After successfully connected with the server, you can run sql queries in the beeline console. For instance,

```java
> SHOW DATABASES;
```

You will see a wall of operation logs, and a result table in the beeline console.

```java
omitted logs
+------------+
| namespace  |
+------------+
| default    |
+------------+
1 row selected (0.2 seconds)
```

### Start Engines

Engines are launched by the server automatically without end users’ attention.

If you use the same user in the above case to create another connection, the engine will be reused. You may notice that the time cost for connection here is much shorter than the last round.

If you use a different user to create a new connection, another engine will be started.

```java
$ bin/beeline -u 'jdbc:hive2://localhost:10009/' -n kentyao
```

This may change depending on the [engine share level]($The-Share-Level-Of-Kyuubi-Engines) you set.

### Close Connections

Close the session between beeline and Kyuubi server by executing `!quit`, for example,

```java
> !quit
Closing: 0: jdbc:hive2://localhost:10009/
```

### Stop Engines

Engines are stop by the server automatically according [engine lifecycle]($The-TTL-Of-Kyuubi-Engines) without end users’ attention. Terminations of connections do not necessarily mean terminations of engines. It depends on both the [engine share level]($The-Share-Level-Of-Kyuubi-Engines) and [engine lifecycle]($The-TTL-Of-Kyuubi-Engines).

Stop Kyuubi
-----------------------------------------------------------------------------------------------------------------------

Stop Kyuubi by running the following in the `$KYUUBI_HOME` directory:

```java
$ bin/kyuubi stop
```

And then, you will see the Kyuubi server waving goodbye to you.

The Kyuubi server will be stopped immediately while the engine will still be alive for a while.

If you start Kyuubi again before the engine terminates itself, it will reconnect to the newly created one.
