[TOC]

Accumulo tables can be used as the source and destination of MapReduce jobs.

General MapReduce configuration
-----------------------------------------------------------------------------------------------------------------------------

### Add Accumulo’s MapReduce API to your dependencies

If you are using Maven, add the following dependency to your `pom.xml` to use Accumulo’s MapReduce API:

```
<dependency>
  <groupId>org.apache.accumulo</groupId>
  <artifactId>accumulo-hadoop-mapreduce</artifactId>
  <version>2.1.2</version>
</dependency>
```

The MapReduce API consists of the following classes:

*   If using Hadoop’s **mapreduce** API:
    *   [org.apache.accumulo.hadoop.mapreduce.AccumuloInputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloInputFormat.html)
    *   [org.apache.accumulo.hadoop.mapreduce.AccumuloOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloOutputFormat.html)
    *   [org.apache.accumulo.hadoop.mapreduce.AccumuloFileOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloFileOutputFormat.html)
*   If using Hadoop’s **mapred** API:
    *   [org.apache.accumulo.hadoop.mapred.AccumuloInputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapred/AccumuloInputFormat.html)
    *   [org.apache.accumulo.hadoop.mapred.AccumuloOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapred/AccumuloOutputFormat.html)
    *   [org.apache.accumulo.hadoop.mapred.AccumuloFileOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapred/AccumuloFileOutputFormat.html)

Before 2.0, the MapReduce API resided in the `org.apache.accumulo.core.client` package of the `accumulo-core` jar. While this old API still exists and can be used, it has been deprecated and will be removed eventually.

### Configure dependencies for your MapReduce job

Before 2.0, Accumulo used the same versions for dependencies (such as Guava) as Hadoop. This allowed MapReduce jobs to run with both Accumulo’s & Hadoop’s dependencies on the classpath.

Since 2.0, Accumulo no longer has the same versions for dependencies as Hadoop. While this allows Accumulo to update its dependencies more frequently, it can cause problems if both Accumulo’s & Hadoop’s dependencies are on the classpath of the MapReduce job. When launching a MapReduce job that uses Accumulo, you should build a [shaded jar](https://maven.apache.org/plugins/maven-shade-plugin/index.html) with all of your dependencies and complete the following steps so YARN only includes Hadoop code (and not all of Hadoop’s dependencies) when running your MapReduce job:

1.  Set `export HADOOP_USE_CLIENT_CLASSLOADER=true` in your environment before submitting your job with `yarn` command.

2.  Set the following in your Job configuration.

    ```
     job.getConfiguration().set("mapreduce.job.classloader", "true");
    ```


Read input from an Accumulo table
---------------------------------------------------------------------------------------------------------------------------------

Follow the steps below to create a MapReduce job that reads from an Accumulo table:

1.  Create a Mapper with the following class parameterization.

    ```
     class MyMapper extends Mapper<Key,Value,WritableComparable,Writable> {
         public void map(Key k, Value v, Context c) {
             // transform key and value data here
         }
     }
    ```

2.  Configure your MapReduce job to use [AccumuloInputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloInputFormat.html).

    ```
     Job job = Job.getInstance();
     job.setInputFormatClass(AccumuloInputFormat.class);
     Properties props = Accumulo.newClientProperties().to("myinstance","zoo1,zoo2")
                             .as("user", "passwd").build();
     AccumuloInputFormat.configure().clientProperties(props).table(table).store(job);
    ```

    [AccumuloInputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloInputFormat.html) has optional settings.

    ```
     List<Range> ranges = new ArrayList<Range>();
     Collection<IteratorSetting.Column> columns = new ArrayList<IteratorSetting.Column>();
     // populate ranges & columns
     IteratorSetting is = new IteratorSetting(30, RexExFilter.class);
     RegExFilter.setRegexs(is, ".*suffix", null, null, null, true);
    
     AccumuloInputFormat.configure().clientProperties(props).table(table)
         .auths(Authorizations.EMPTY) // optional: default to user's auths if not set
         .ranges(ranges)              // optional: only read specified ranges
         .fetchColumns(columns)       // optional: only read specified columns
         .addIterator(is)             // optional: add iterator that matches row IDs
         .store(job);
    ```

    [AccumuloInputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloInputFormat.html) can also be configured to read from multiple Accumulo tables.

    ```
     Job job = Job.getInstance();
     job.setInputFormatClass(AccumuloInputFormat.class);
     Properties props = Accumulo.newClientProperties().to("myinstance","zoo1,zoo2")
                             .as("user", "passwd").build();
     AccumuloInputFormat.configure().clientProperties(props)
         .table("table1").auths(Authorizations.EMPTY).ranges(tableOneRanges)
         .table("table2").auths(Authorizations.EMPTY).ranges(tableTwoRanges)
         .store(job);
    ```

    If reading from multiple tables, the table name can be retrieved from the input split:

    ```
     class MyMapper extends Mapper<Key,Value,WritableComparable,Writable> {
         public void map(Key k, Value v, Context c) {
             RangeInputSplit split = (RangeInputSplit)c.getInputSplit();
             String tableName = split.getTableName();
             // do something with table name
         }
     }
    ```


Write output to an Accumulo table
---------------------------------------------------------------------------------------------------------------------------------

Follow the steps below to write to an Accumulo table from a MapReduce job.

1.  Create a Reducer with the following class parameterization. The key emitted from the Reducer identifies the table to which the mutation is sent. This allows a single Reducer to write to more than one table if desired. A default table can be configured using the [AccumuloOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloOutputFormat.html), in which case the output table name does not have to be passed to the Context object within the Reducer.

    ```
     class MyReducer extends Reducer<WritableComparable, Writable, Text, Mutation> {
         public void reduce(WritableComparable key, Iterable<Text> values, Context c) {
             Mutation m;
             // create the mutation based on input key and value
             c.write(new Text("output-table"), m);
         }
     }
    ```

    The Text object passed as the output should contain the name of the table to which this mutation should be applied. The Text can be null in which case the mutation will be applied to the default table name specified in the [AccumuloOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloOutputFormat.html) options.

2.  Configure your MapReduce job to use [AccumuloOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloOutputFormat.html).

    ```
     Job job = Job.getInstance();
     job.setOutputFormatClass(AccumuloOutputFormat.class);
     Properties props = Accumulo.newClientProperties().to("myinstance","zoo1,zoo2")
                             .as("user", "passwd").build();
     AccumuloOutputFormat.configure().clientProperties(props)
         .defaultTable("mytable").store(job);
    ```


Write output to RFiles in HDFS
---------------------------------------------------------------------------------------------------------------------------

Follow the steps below to have a MapReduce job output to RFiles in HDFS. These files can then be bulk imported into Accumulo:

1.  Create a Mapper or Reducer with `Key` & `Value` as output parameters.

    ```
     class MyReducer extends Reducer<WritableComparable, Writable, Key, Value> {
         public void reduce(WritableComparable key, Iterable<Text> values, Context c) {
             Key key;
             Value value;
             // create Key & Value based on input
             c.write(key, value);
         }
     }
    ```

2.  Configure your MapReduce job to use [AccumuloFileOutputFormat](https://static.javadoc.io/org.apache.accumulo/accumulo-hadoop-mapreduce/2.1.2/org/apache/accumulo/hadoop/mapreduce/AccumuloFileOutputFormat.html).

    ```
     Job job = Job.getInstance();
     job.setOutputFormatClass(AccumuloFileOutputFormat.class);
     AccumuloFileOutputFormat.configure()
         .outputPath(new Path("hdfs://localhost:8020/myoutput/")).store(job);
    ```


Example Code
---------------------------------------------------------------------------------------

The [Accumulo Examples repo](https://github.com/apache/accumulo-examples/) has several MapReduce examples:

*   [wordcount](https://github.com/apache/accumulo-examples/blob/main/docs/wordcount.md) - Uses MapReduce and Accumulo to do a word count on text files
*   [regex](https://github.com/apache/accumulo-examples/blob/main/docs/regex.md) - Uses MapReduce and Accumulo to find data using regular expressions
*   [rowhash](https://github.com/apache/accumulo-examples/blob/main/docs/rowhash.md) - Uses MapReduce to read a table and write to a new column in the same table
*   [tabletofile](https://github.com/apache/accumulo-examples/blob/main/docs/tabletofile.md) - Uses MapReduce to read a table and write one of its columns to a file in HDFS
*   [uniquecols](https://github.com/apache/accumulo-examples/blob/main/docs/uniquecols.md) - Uses MapReduce to count unique columns in Accumulo
