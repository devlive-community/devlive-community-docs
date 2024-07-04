[TOC]


## Spark Streaming

Structured Streaming reads are based on Hudi's Incremental Query feature, therefore streaming read can return data for which
commits and base files were not yet removed by the cleaner. You can control commits retention time.

> Scala

```scala
// spark-shell
// reload data
df.write.format("hudi").
  options(getQuickstartWriteConfigs).
  option("hoodie.datasource.write.precombine.field", "ts").
  option("hoodie.datasource.write.recordkey.field", "uuid").
  option("hoodie.datasource.write.partitionpath.field", "partitionpath").
  option("hoodie.table.name", tableName).
  mode(Overwrite).
  save(basePath)

// read stream and output results to console
spark.readStream.
  format("hudi").
  load(basePath).
  writeStream.
  format("console").
  start()

// read stream to streaming df
val df = spark.readStream.
        format("hudi").
        load(basePath)

```

> Python

```python
# pyspark
# reload data
inserts = sc._jvm.org.apache.hudi.QuickstartUtils.convertToStringList(
    dataGen.generateInserts(10))
df = spark.read.json(spark.sparkContext.parallelize(inserts, 2))

hudi_options = {
    'hoodie.table.name': tableName,
    'hoodie.datasource.write.recordkey.field': 'uuid',
    'hoodie.datasource.write.partitionpath.field': 'partitionpath',
    'hoodie.datasource.write.table.name': tableName,
    'hoodie.datasource.write.operation': 'upsert',
    'hoodie.datasource.write.precombine.field': 'ts',
    'hoodie.upsert.shuffle.parallelism': 2,
    'hoodie.insert.shuffle.parallelism': 2
}

df.write.format("hudi"). \
    options(**hudi_options). \
    mode("overwrite"). \
    save(basePath)

# read stream to streaming df
df = spark.readStream \
    .format("hudi") \
    .load(basePath)

# ead stream and output results to console
spark.readStream \
    .format("hudi") \
    .load(basePath) \
    .writeStream \
    .format("console") \
    .start()

```

> Spark SQL can be used within ForeachBatch sink to do INSERT, UPDATE, DELETE and MERGE INTO.
> Target table must exist before write.

