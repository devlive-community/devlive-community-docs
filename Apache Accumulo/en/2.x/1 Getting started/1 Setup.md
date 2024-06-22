[TOC]

User Manual (2.x and 3.x)
-------------------------

Starting with Accumulo 2.0, the user manual now lives on the website as a series of web pages. Previously, it was one large pdf document that was only generated during a release. The user manual can now be updated very quickly and indexed for searching across many webpages.

The manual can now be searched using the [Search link](https://accumulo.apache.org/search) at the top of the website or navigated by clicking the links to the left. If you are new to Accumulo, follow the instructions below to get started. For detailed instructions, see the [in-depth installation guide](https://accumulo.apache.org/docs/2.x/administration/in-depth-install).

Master/Manager naming
-------------------------------------------------------------------------------------------------------------

As of release 2.1, all references to “master” have been changed to “manager.” If you are using/installing a release prior to 2.1, substitute “master” in place of “manager” for any property name, file name, or process name referenced in this documentation.

Setup for testing or development
------------------------------------------------------------------------------------------------------------------------------------

If you are setting up Accumulo for **testing or development,** consider using the following tools:

*   [Uno](https://github.com/apache/fluo-uno) sets up Accumulo on a single machine for development
*   [Muchos](https://github.com/apache/fluo-muchos) sets up Accumulo on a cluster (optionally launched in Amazon EC2 and Microsoft Azure VM)

If you are setting up Accumulo for a **production** environment, follow the instructions below.

Setup for Production
------------------------------------------------------------------------------------------------------------

Either [download](https://accumulo.apache.org/downloads) or [build](https://github.com/apache/accumulo/blob/main/README.md#building) a binary distribution of Accumulo from source code and unpack as follows.

```
tar xzf /path/to/accumulo-2.1.2-bin.tar.gz
cd accumulo-2.1.2
```

There are four scripts in the `bin` directory of the tarball distribution that are used to manage Accumulo:

1.  `accumulo` - Runs Accumulo command-line tools and starts Accumulo processes
2.  `accumulo-service` - Runs individual Accumulo processes as background services
3.  `accumulo-cluster` - Manages Accumulo cluster on a single node or several nodes
4.  `accumulo-util` - Accumulo utilities for building native libraries, running jars, etc.

These scripts will be used in the remaining instructions to configure and run Accumulo. For convenience, consider adding `accumulo-2.1.2/bin/` to your shell’s path.

Configuring Accumulo
------------------------------------------------------------------------------------------------------------

Accumulo requires running [Zookeeper](https://zookeeper.apache.org/) and [HDFS](https://hadoop.apache.org/) instances which should be set up before configuring Accumulo.

**Important note:** If using [Erasure Coding](https://hadoop.apache.org/docs/r3.2.0/hadoop-project-dist/hadoop-hdfs/HDFSErasureCoding.html) (EC), data loss will occur unless it is configured properly for Accumulo. Please see the [Erasure Coding guide]($Erasure-Coding) for more information.

The primary configuration files for Accumulo are [accumulo.properties]($Configuration-Files#accumuloproperties), [accumulo-env.sh]($Configuration-Files#accumulo-envsh), and [accumulo-client.properties]($Configuration-Files#accumulo-clientproperties) which are located in the `conf/` directory.

The [accumulo.properties]($Configuration-Files#accumuloproperties) file configures Accumulo server processes (i.e. tablet server, manager, monitor, etc). Follow these steps to set it up:

1.  Run `accumulo-util build-native` to build native code. If this command fails, disable native maps by setting [tserver.memory.maps.native.enabled]($Server-Properties-2.x#tserver_memory_maps_native_enabled) to `false`.

2.  Set [instance.volumes]($Server-Properties-3.x#instance_volumes) to HDFS location where Accumulo will store data. If your namenode is running at 192.168.1.9:8020, and you want to store data in `/accumulo` in HDFS, then set [instance.volumes]($Server-Properties-3.x#instance_volumes) to `hdfs://192.168.1.9:8020/accumulo`.

3.  Set [instance.zookeeper.host]($Server-Properties-3.x#instance_zookeeper_host) to the location of your Zookeepers

4.  (Optional) Change [instance.secret]($Server-Properties-3.x#instance_secret) (which is used by Accumulo processes to communicate) from the default. This value should match on all servers.


The [accumulo-env.sh]($Configuration-Files#accumulo-envsh) file sets up environment variables needed by Accumulo:

1.  Set `HADOOP_HOME` and `ZOOKEEPER_HOME` to the location of your Hadoop and Zookeeper installations. Accumulo will use these locations to find Hadoop and Zookeeper jars and add them to your `CLASSPATH` variable. If you are running a vendor-specific release of Hadoop or Zookeeper, you may need to modify how the `CLASSPATH` variable is built in [accumulo-env.sh]($Configuration-Files#accumulo-envsh). If Accumulo has problems loading classes when you start it, run `accumulo classpath` to print Accumulo’s classpath.

2.  Accumulo tablet servers are configured by default to use 1GB of memory (768MB is allocated to JVM and 256MB is allocated for native maps). Native maps are allocated memory equal to 33% of the tserver JVM heap. The table below can be used if you would like to change tserver memory usage in the `JAVA_OPTS` section of [accumulo-env.sh]($Configuration-Files#accumulo-envsh):

    | Native? | 512MB | 1GB | 2GB | 3GB |
        | --- | --- | --- | --- | --- |
    | Yes | \-Xmx384m -Xms384m | \-Xmx768m -Xms768m | \-Xmx1536m -Xms1536m | \-Xmx2g -Xms2g |
    | No | \-Xmx512m -Xms512m | \-Xmx1g -Xms1g | \-Xmx2g -Xms2g | \-Xmx3g -Xms3g |

3.  (Optional) Review the memory settings for the Accumulo manager, garbage collector, and monitor in the `JAVA_OPTS` section of [accumulo-env.sh]($Configuration-Files#accumulo-envsh).


The [accumulo-client.properties]($Configuration-Files#accumulo-clientproperties) file is used by the Accumulo shell and can be passed to Accumulo clients to simplify connecting to Accumulo. Below are steps to configure it.

1.  Set [instance.name]($Client-Properties-2.x#instance_name) and [instance.zookeepers]($Client-Properties-2.x#instance_zookeepers) to the Accumulo instance and zookeeper connection string of your instance.

2.  Pick an authentication type and set [auth.type]($Client-Properties-2.x#auth_type) accordingly. The most common `auth.type` is `password` which requires [auth.principal]($Client-Properties-2.x#auth_principal) to be set and [auth.token]($Client-Properties-2.x#auth_token) to be set the password of `auth.principal`. For the Accumulo shell, `auth.token` can be commented out and the shell will prompt you for the password of `auth.principal` at login.


Initialization
------------------------------------------------------------------------------------------------

Accumulo needs to initialize the locations where it stores data in Zookeeper and HDFS.

Note: Initialization only needs to be performed once for an instance - if you are performing an upgrade you should not run the initialization command a second time unless you really want a new instance.

The following command will perform the initialization.

The initialization command will prompt for the following information.

*   **Instance name** : This is the name of the Accumulo instance and its Accumulo clients need to know it in order to connect.
*   **Root password** : Initialization sets up an initial Accumulo root user and prompts for its password. This information will be needed to later connect to Accumulo.

Run Accumulo
--------------------------------------------------------------------------------------------

There are several methods for running Accumulo:

1.  Run Accumulo processes using `accumulo` command which runs processes in foreground and will not redirect stderr/stdout. Useful for creating init.d scripts that run Accumulo.

2.  Run individual Accumulo processes as services using `accumulo-service` which uses `accumulo` command but backgrounds processes, redirects stderr/stdout and manages pid files. This is useful if you are using a cluster management tool (i.e. Ansible, Salt, etc).

3.  Run an Accumulo cluster on one or more nodes using `accumulo-cluster` (which uses `accumulo-service` to run services). Useful for local development and testing or if you are not using your own cluster management tool in production.


Each method above has instructions below.

### Run individual Accumulo processes

Start Accumulo processes (tserver, manager, monitor, etc) using the accumulo command followed by the service name. For example, to start only the tserver, run:

The process will run in the foreground. Use ctrl-c to quit.

For a fully operational instance, each individual service will need to be started.

### Run individual Accumulo services

Start individual Accumulo processes (tserver, master, monitor, etc.) as a background service using the example accumulo-service script followed by the service name. For example, to start only the tserver, run:

```
accumulo-service tserver start
```

For a fully operational instance, each individual service will need to be started.

### Run an Accumulo cluster

Before using the `accumulo-cluster` script to start the cluster, additional configuration files may need to be created. Use the command below to create them from provided templates:

```
accumulo-cluster create-config
```

This creates a yaml configuration file in the `conf/` directory named `cluster.yaml` that contains the node names where Accumulo services are run on your cluster. By default, all services are configured to `localhost`. If you are running a single-node Accumulo cluster, these files do not need to be changed and the next section should be skipped. The external compaction services exist in the file but are commented out as they are optional.

#### Multi-node configuration

If you are running an Accumulo cluster on multiple nodes, the `conf/cluster.yaml` file contains sections that should be configured with a list of node names in yaml format:

*   [manager]($Configuration-Files#managers) : Accumulo primary coordinating process. Must specify one node. Can specify a few for fault tolerance.
*   [gc]($Configuration-Files#gc) : Accumulo garbage collector. Must specify one node. Can specify a few for fault tolerance.
*   [monitor]($Configuration-Files#monitor) : Node where Accumulo monitoring web server is run.
*   [tserver]($Configuration-Files#tservers) : Accumulo worker processes. List all of the nodes where tablet servers should run.
*   [sserver]($Configuration-Files#sserver) : Optional. List of all nodes where scan servers should run.
*   [compaction.coordinator]($Configuration-Files#compaction%20coordinator) : Optional. Must specify one node. Can specify a few for fault tolerance.
*   [compaction.compactor]($Configuration-Files#compaction%20compactor) : Optional. Accumulo external compactor processes. List of all nodes where compactors should run.

The Accumulo, Hadoop, and Zookeeper software should be present at the same location on every node. Also, the files in the `conf` directory must be copied to every node. There are many ways to replicate the software and configuration, two possible tools that can help replicate software and/or config are [pdcp](https://code.google.com/p/pdsh/) and [prsync](https://code.google.com/p/parallel-ssh/).

The `accumulo-cluster` script uses ssh to start processes on remote nodes. Before attempting to start Accumulo, [passwordless ssh](https://www.google.com/search?q=hadoop+passwordless+ssh&ie=utf-8&oe=utf-8) must be setup on the cluster.

#### Start cluster

After configuring and initializing Accumulo, use the following command to start the cluster using the provided cluster management script:

First steps
------------------------------------------------------------------------------------------

Once you have started Accumulo, use the following command to run the Accumulo shell:

Use your web browser to connect the Accumulo monitor page on port 9995.

```
http://<hostname in conf/monitor>:9995/
```

Stopping Accumulo
------------------------------------------------------------------------------------------------------

When finished, use the following commands to stop Accumulo:

*   Stop an individual Accumulo service: `accumulo-service tserver stop`
*   Stop Accumulo cluster: `accumulo-cluster stop`
