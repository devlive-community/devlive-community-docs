[TOC]

Kyuubi supports Apache Hive beeline that works with Kyuubi server. Hive beeline is a [SQLLine CLI](https://sqlline.sourceforge.net/) based on the [Hive JDBC Driver](https://kyuubi.readthedocs.io/en/v1.9.1/client/jdbc/hive_jdbc.html).

Prerequisites
-------------

- Kyuubi server installed and launched.
- Hive beeline installed

>  Kyuubi does not support embedded mode which beeline and server run in the same process.
It always uses remote mode for connecting beeline with a separate server process over thrift.

> The document you are visiting now is incomplete, please help kyuubi community to fix it if appropriate for you.
