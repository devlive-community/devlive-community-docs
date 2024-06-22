[TOC]

The [Accumulo Proxy](https://github.com/apache/accumulo-proxy/) allows the interaction with Accumulo with languages other than Java. A proxy server is provided in the codebase and a client can further be generated. The proxy API can also be used instead of the traditional [AccumuloClient](https://static.javadoc.io/org.apache.accumulo/accumulo-core/2.1.2/org/apache/accumulo/core/client/AccumuloClient.html) class to provide a single TCP port in which clients can be securely routed through a firewall, without requiring access to all tablet servers in the cluster.

Prerequisites
-------------------------------------------------------------------------------------

The proxy server can live on any node in which the basic client API would work. That means it must be able to communicate with the Manager, ZooKeepers, NameNode, and the DataNodes. A proxy client only needs the ability to communicate with the proxy server.

Running the Proxy Server
-----------------------------------------------------------------------------------------------------------

To run [Accumulo Proxy](https://github.com/apache/accumulo-proxy/) server, first clone the repository:

```
git clone https://github.com/apache/accumulo-proxy
```

Next, follow the instructions in the Proxy [README.md](https://github.com/apache/accumulo-proxy/blob/main/README.md) or use [Uno](https://github.com/apache/fluo-uno/) to run the proxy.

To run the Proxy using [Uno](https://github.com/apache/fluo-uno/), configure `uno.conf` to start the Proxy by setting the configuration below:

```
export POST_RUN_PLUGINS="accumulo-proxy"
export PROXY_REPO=/path/to/accumulo-proxy
```

Proxy Client Examples
-----------------------------------------------------------------------------------------------------

The following examples show proxy clients written in Java, Ruby, and Python.

### Ruby

The [Accumulo Proxy](https://github.com/apache/accumulo-proxy/) repo has an example [ruby client](https://github.com/apache/accumulo-proxy/src/main/ruby/client.rb) along with [instructions](https://github.com/apache/accumulo-proxy/#create-an-accumulo-client-using-ruby) on how to run it.

### Python

The [Accumulo Proxy](https://github.com/apache/accumulo-proxy/) repo has two example Python scripts that can be run using these [instructions](https://github.com/apache/accumulo-proxy/#create-an-accumulo-client-using-python):

*   [basic client](https://github.com/apache/accumulo-proxy/blob/main/src/main/python/basic_client.py) - creates a table, writes data to it, and then reads it
*   [namespace client](https://github.com/apache/accumulo-proxy/blob/main/src/main/python/namespace_client.py) - shows how to manage Accumulo namespaces.

### Java[](https://accumulo.apache.org/docs/2.x/development/proxy#java)

Users may want to write a [Java client](https://github.com/apache/accumulo-proxy/docs/java_client.md) to the proxy to restrict access to the cluster.
