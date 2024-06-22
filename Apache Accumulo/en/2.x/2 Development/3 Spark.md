[TOC]

[Apache Spark](https://spark.apache.org/) applications can read from and write to Accumulo tables.

Before reading this documentation, it may help to review the [MapReduce]($MapReduce) documentation as API created for MapReduce jobs is used by Spark.

This documentation references code from the Accumulo [Spark example](https://github.com/apache/accumulo-examples/tree/main/spark).

General configuration
-----------------------------------------------------------------------------------------------------

1.  Create a [shaded jar](https://maven.apache.org/plugins/maven-shade-plugin/index.html) with your Spark code and all of your dependencies (excluding Spark and Hadoop). When creating the shaded jar, you should relocate Guava as Accumulo uses a different version. The [pom.xml](https://github.com/apache/accumulo-examples/blob/main/pom.xml) in the [Spark example](https://github.com/apache/accumulo-examples/tree/main/spark) is a good reference and can be used as a starting point for a Spark application.

2.  Submit the job by running `spark-submit` with your shaded jar. You should pass in the location of your `accumulo-client.properties` that will be used to connect to your Accumulo instance.

    ```
     $SPARK_HOME/bin/spark-submit \
       --class com.my.spark.job.MainClass \
       --master yarn \
       --deploy-mode client \
       /path/to/spark-job-shaded.jar \
       /path/to/accumulo-client.properties
    ```


Reading from Accumulo table
-----------------------------------------------------------------------------------------------------------------

Apache Spark can read from an Accumulo table by using [AccumuloInputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloInputFormat.html).

```
Job job = Job.getInstance();
AccumuloInputFormat.configure().clientProperties(props).table(inputTable).store(job);
JavaPairRDD<Key,Value> data = sc.newAPIHadoopRDD(job.getConfiguration(),
    AccumuloInputFormat.class, Key.class, Value.class);
```

Writing to Accumulo table
-------------------------------------------------------------------------------------------------------------

There are two ways to write to an Accumulo table in Spark applications.

### Use a BatchWriter

Write your data to Accumulo by creating an AccumuloClient for each partition and writing all data in the partition using a BatchWriter.

```
// Spark will automatically serialize this properties object and send it to each partition
Properties props = Accumulo.newClientProperties()
                    .from("/path/to/accumulo-client.properties").build();
JavaPairRDD<Key, Value> dataToWrite = ... ;
dataToWrite.foreachPartition(iter -> {
  // Create client inside partition so that Spark does not attempt to serialize it.
  try (AccumuloClient client = Accumulo.newClient().from(props).build();
       BatchWriter bw = client.createBatchWriter(outputTable)) {
    iter.forEachRemaining(kv -> {
      Key key = kv._1;
      Value val = kv._2;
      Mutation m = new Mutation(key.getRow());
      m.at().family(key.getColumnFamily()).qualifier(key.getColumnQualifier())
          .visibility(key.getColumnVisibility()).timestamp(key.getTimestamp()).put(val);
      bw.addMutation(m);
    });
  }
});
```

### Using Bulk Import

Partition your data and write it to RFiles. The [AccumuloRangePartitioner](https://github.com/apache/accumulo-examples/blob/main/spark/src/main/java/org/apache/accumulo/spark/CopyPlus5K.java#L44) found in the Accumulo Spark example can be used for partitioning data. After your data has been written to an output directory using [AccumuloFileOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloFileOutputFormat.html) as RFiles, bulk import this directory into Accumulo.

```
// Write Spark output to HDFS
JavaPairRDD<Key, Value> dataToWrite = ... ;
Job job = Job.getInstance();
AccumuloFileOutputFormat.configure().outputPath(outputDir).store(job);
Partitioner partitioner = new AccumuloRangePartitioner("3", "7");
JavaPairRDD<Key, Value> partData = dataPlus5K.repartitionAndSortWithinPartitions(partitioner);
partData.saveAsNewAPIHadoopFile(outputDir.toString(), Key.class, Value.class,
    AccumuloFileOutputFormat.class);

// Bulk import RFiles in HDFS into Accumulo
try (AccumuloClient client = Accumulo.newClient().from(props).build()) {
  client.tableOperations().importDirectory(outputDir.toString()).to(outputTable).load();
}
```

Reference
-----------------------------------------------------------------------------

*   [Spark example](https://github.com/apache/accumulo-examples/tree/main/spark) - Example Spark application that reads from and writes to Accumulo
*   [MapReduce]($MapReduce) - Documentation on reading/writing to Accumulo using MapReduce
*   [Apache Spark](https://spark.apache.org/) - Spark project website
