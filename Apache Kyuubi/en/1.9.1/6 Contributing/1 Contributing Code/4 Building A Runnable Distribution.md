[TOC]


To create a Kyuubi distribution like those distributed by [Kyuubi Release Page](https://kyuubi.apache.org/releases.html),
and that is laid out to be runnable, use `./build/dist` in the project root directory.

For more information on usage, run `./build/dist --help`

```logtalk
./build/dist - Tool for making binary distributions of Kyuubi

Usage:
+----------------------------------------------------------------------------------------------+
| ./build/dist [--name <custom_name>] [--tgz] [--web-ui] [--flink-provided] [--hive-provided]  |
|              [--spark-provided] [--mvn <maven_executable>] <maven build options>             |
+----------------------------------------------------------------------------------------------+
name:           -  custom binary name, using project version if undefined
tgz:            -  whether to make a whole bundled package
web-ui:         -  whether to include web ui
flink-provided: -  whether to make a package without Flink binary
hive-provided:  -  whether to make a package without Hive binary
spark-provided: -  whether to make a package without Spark binary
mvn:            -  external maven executable location
```

For instance,

```bash
./build/dist --name custom-name --tgz
```

This results in a Kyuubi distribution named `apache-kyuubi-{version}-bin-custom-name.tgz` for you.

If you are planing to deploy Kyuubi where `spark`/`flink`/`hive` is provided, in other word, it's not required to bundle spark/flink/hive binary, use

```bash
./build/dist --tgz --spark-provided --flink-provided --hive-provided
```

Then you will get a Kyuubi distribution without spark/flink/hive binary named `apache-kyuubi-{version}-bin.tgz`.

