[TOC]


[Gluten](https://oap-project.github.io/gluten/) is a Spark plugin developed by Intel, designed to accelerate Apache Spark with native libraries. Currently, only CentOS 7/8 and Ubuntu 20.04/22.04, along with Spark 3.2/3.3/3.4, are supported. Users can employ the following methods to utilize the Gluten with Velox native libraries.

## Building(with velox Backend)

### Build gluten velox backend package

Git clone gluten project, use gluten build script `buildbundle-veloxbe.sh`, and target package is in `/path/to/gluten/package/target/`

```bash
git clone https://github.com/oap-project/gluten.git
cd /path/to/gluten

## The script builds two jars for spark 3.2.x, 3.3.x, and 3.4.x.
./dev/buildbundle-veloxbe.sh
```

## Usage

You can use Gluten to accelerate Spark by following steps.

### Installing

Add gluten jar: `copy /path/to/gluten/package/target/gluten-velox-bundle-spark3.x_2.12-*.jar $SPARK_HOME/jars/` or specified to `spark.jars` configuration

### Configure

Add the following minimal configuration into `spark-defaults.conf`:

```properties
spark.plugins=io.glutenproject.GlutenPlugin
spark.memory.offHeap.size=20g
spark.memory.offHeap.enabled=true
spark.shuffle.manager=org.apache.spark.shuffle.sort.ColumnarShuffleManager
```

For more configuration can be found in the doc of [Configuration](https://oap-project.github.io/gluten/Configuration.html).

