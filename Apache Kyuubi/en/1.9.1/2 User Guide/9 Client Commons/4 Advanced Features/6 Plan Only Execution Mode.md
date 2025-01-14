[TOC]



Plan only execution mode currently only supports spark and flink engine.

Configure the kyuubi.operation.plan.only.mode parameter, the value can be 'parse', 'analyze', 'optimize', 'optimize_with_stats', 'physical', 'execution', or 'none', when it is 'none', indicate to the statement will be fully executed, otherwise only way without executing the query. Different engines currently support different modes, the spark engine supports all modes, and the flink engine supports 'parse', 'physical', and 'execution', other engines do not support plan-only mode currently, and supports application-level and session-level parameter settings, which are used in the following ways.

## Application-level parameter setting

You can add parameters to the URL when establishing a JDBC connection, the parameter is kyuubi.operation.plan.only.mode=parse/analyze/optimize.
JDBC URLs have the following format:

```shell
jdbc:hive2://<host>:<port>/<dbName>;<sessionVars>?kyuubi.operation.plan.only.mode=parse/analyze/optimize/optimize_with_stats/physical/execution/none;<kyuubiConfs>#<[spark|hive]Vars>
```

Refer to [hive_jdbc doc]($Hive-JDBC-Driver) for details of others parameters

### Example:

Using beeline tool to connect to the local service, the Shell command is:

```shell
beeline -u 'jdbc:hive2://0.0.0.0:10009/default?kyuubi.operation.plan.only.mode=parse' -n {user_name}
```

Running the following SQL:

```sql
SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id
```

The results are as follows:

```shell
# SQL:
0: jdbc:hive2://0.0.0.0:10009/default> SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;

#Result:
+----------------------------------------------------+
|                        plan                        |
+----------------------------------------------------+
| 'Project [*]
+- 'Join LeftOuter, ('t1.id = 't2.id)
   :- 'UnresolvedRelation [t1], [], false
   +- 'UnresolvedRelation [t2], [], false
 |
+----------------------------------------------------+
1 row selected (3.008 seconds)
0: jdbc:hive2://0.0.0.0:10009/default>
```

## Session-level parameter setting

You can also set the kyuubi.operation.plan.only.mode parameter by executing the set command after the connection has been established

```shell
beeline -u 'jdbc:hive2://0.0.0.0:10009/default' -n {user_name}
```

Running the following SQL:

```sql
set kyuubi.operation.plan.only.mode=parse;
SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id
```

The results are as follows:

```shell
#set command:
0: jdbc:hive2://0.0.0.0:10009/default> set kyuubi.operation.plan.only.mode=parse;

#set command result:
+----------------------------------+--------+
|               key                | value  |
+----------------------------------+--------+
| kyuubi.operation.plan.only.mode  | parse  |
+----------------------------------+--------+
1 row selected (0.568 seconds)

#execute SQL:
0: jdbc:hive2://0.0.0.0:10009/default> SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;

# SQL result:
+----------------------------------------------------+
|                        plan                        |
+----------------------------------------------------+
| 'Project [*]
+- 'Join LeftOuter, ('t1.id = 't2.id)
   :- 'UnresolvedRelation [t1], [], false
   +- 'UnresolvedRelation [t2], [], false
 |
+----------------------------------------------------+
1 row selected (0.404 seconds)
0: jdbc:hive2://0.0.0.0:10009/default>
```


