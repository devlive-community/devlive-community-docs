[TOC]

Accumulo has the following configuration files which can be found in the `conf/` directory of the Accumulo release tarball.

accumulo.properties
--------------------------------------------------------------------------------------------------

The [accumulo.properties](https://github.com/apache/accumulo/blob/main/assemble/conf/accumulo.properties) file configures Accumulo server processes using [server properties]($Server-Properties-2.x). This file can be found in the `conf/` directory. It is needed on every host that runs Accumulo processes. Therefore, any configuration should be replicated to all hosts of the Accumulo cluster. If a property is not configured here, it might have been [configured another way]($Configuration-Overview). See the [quick start]($Setup#configuring-accumulo) for help with configuring this file.

accumulo-client.properties
----------------------------------------------------------------------------------------------------------------

The `accumulo-client.properties` file configures Accumulo client processes using [client properties]($Client-Properties-2.x). If `accumulo shell` is run without arguments, the Accumulo connection information in this file will be used. This file can be used to create an AccumuloClient in Java using the following code:

```
AccumuloClient client = Accumulo.newClient().from("/path/to/accumulo-client.properties").build();
```

See the [quick start]($Setup#configuring-accumulo) for help with configuring this file.

accumulo-env.sh
------------------------------------------------------------------------------------------

The [accumulo-env.sh](https://github.com/apache/accumulo/blob/main/assemble/conf/accumulo-env.sh) file configures the Java classpath and JVM options needed to run Accumulo processes. See the [quick start]($Setup#configuring-accumulo) for help with configuring this file.

Log configuration files
-----------------------------------------------------------------------------------------------------------

### log4j2-service.properties

Since 2.1, the [log4j2-service.properties](https://github.com/apache/accumulo/blob/main/assemble/conf/log4j2-service.properties) file configures logging for most Accumulo services (i.e [Manager]($Design#manager), [Tablet Server]($Design#tablet-server), [Garbage Collector]($Design#garbage-collector), [Monitor]($Design#monitor)). Prior to 2.1 this file was named `log4j-service.properties` and did not apply to the [Monitor]($Design#monitor) which was configured in a separate `log4j-monitor.properties`.

### log4j2.properties

The [log4j2.properties](https://github.com/apache/accumulo/blob/main/assemble/conf/log4j2.properties) file configures logging for Accumulo commands (i.e `accumulo init`, `accumulo shell`, etc).

cluster.yaml
------------------------------------------------------------------------------------

The `accumulo-cluster` script uses the `cluster.yaml` file to determine where Accumulo processes should be run. This file is not in the `conf/` directory of the Accumulo release tarball by default. It can be created by running the command `accumulo-cluster create-config`. The `cluster.yaml` file contains the following sections:

### gc

Contains a list of hosts where [Garbage Collector]($Design#garbage-collector) processes should run. While only one host is needed, others can be specified to run standby Garbage Collectors that can take over if the lead Garbage Collector fails.

### manager

Contains a list of hosts where [Manager]($Design#manager) processes should run. While only one host is needed, others can be specified to run on standby Managers that can take over if the lead Manager fails.

### monitor

Contains a list of hosts where [Monitor]($Design#monitor) processes should run. While only one host is needed, others can be specified to run standby Monitors that can take over if the lead Monitor fails.

### tserver

Contains list of hosts where [Tablet Server]($Design#tablet-server) processes should run. While only one host is needed, it is recommended that multiple tablet servers are run for improved fault tolerance and performance.

### sserver

Contains a list of hosts where [ScanServer]($Design#scan-server-experimental) processes should run. While only one host is needed, it is recommended that multiple ScanServers are run for improved performance.

### compaction coordinator

Contains a list of hosts where [CompactionCoordinator]($Design#compaction-coordinator-experimental) processes should run. While only one host is needed, others can be specified to run standby CompactionCoordinators that can take over if the lead CompactionCoordinator fails.

### compaction compactor

Contains a list of hosts where [Compactor]($Design#compactor-experimental) processes should run. While only one host is needed, it is recommended that multiple Compactors are run for improved external compaction performance.
