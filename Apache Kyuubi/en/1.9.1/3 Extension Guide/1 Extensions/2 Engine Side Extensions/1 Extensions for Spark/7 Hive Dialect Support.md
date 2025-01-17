[TOC]


Hive Dialect plugin aims to provide Hive Dialect support to Spark's JDBC source.
It will auto registered to Spark and applied to JDBC sources with url prefix of `jdbc:hive2://` or `jdbc:kyuubi://`.

Hive Dialect helps to solve failures access Kyuubi. It fails and unexpected results when querying data from Kyuubi as JDBC source with Hive JDBC Driver or Kyuubi Hive JDBC Driver in Spark, as Spark JDBC provides no Hive Dialect support out of box and quoting columns and other identifiers in ANSI as "table.column" rather than in HiveSQL style as \`table\`.\`column\`.

## Features

- quote identifier in Hive SQL style

  eg. Quote `table.column` in \`table\`.\`column\`

## Usage

1. Get the Kyuubi Hive Dialect Extension jar
    1. compile the extension by executing `build/mvn clean package -pl :kyuubi-extension-spark-jdbc-dialect_2.12 -DskipTests`
    2. get the extension jar under `extensions/spark/kyuubi-extension-spark-jdbc-dialect/target`
    3. If you like, you can compile the extension jar with the corresponding Maven's profile on you compile command, i.e. you can get extension jar for Spark 3.5 by compiling with `-Pspark-3.5`
2. Put the Kyuubi Hive Dialect Extension jar `kyuubi-extension-spark-jdbc-dialect_-*.jar` into `$SPARK_HOME/jars`
3. Enable `KyuubiSparkJdbcDialectExtension`, by setting `spark.sql.extensions=org.apache.spark.sql.dialect.KyuubiSparkJdbcDialectExtension`, i.e.
    - add a config into `$SPARK_HOME/conf/spark-defaults.conf`
    - or add setting config in SparkSession builder

