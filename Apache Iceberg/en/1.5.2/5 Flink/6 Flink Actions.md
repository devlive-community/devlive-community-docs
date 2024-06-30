[TOC]

## Rewrite files action.

Iceberg provides API to rewrite small files into large files by submitting Flink batch jobs. The behavior of this Flink action is the same as Spark's [rewriteDataFiles]($Maintenance#compact-data-files).

```java
import org.apache.iceberg.flink.actions.Actions;

TableLoader tableLoader = TableLoader.fromHadoopTable("hdfs://nn:8020/warehouse/path");
Table table = tableLoader.loadTable();
RewriteDataFilesActionResult result = Actions.forTable(table)
        .rewriteDataFiles()
        .execute();
```

For more details of the rewrite files action, please refer to [RewriteDataFilesAction](https://iceberg.apache.org/javadoc/1.5.2/org/apache/iceberg/flink/actions/RewriteDataFilesAction.html)
