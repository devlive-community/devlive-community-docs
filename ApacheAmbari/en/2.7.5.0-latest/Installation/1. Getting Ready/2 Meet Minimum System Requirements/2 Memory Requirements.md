[TOC]

The Ambari host should have at least 1 GB RAM, with 500 MB free.

To check available memory on any host, run:

```bash
free -m
```

If you plan to install the Ambari Metrics Service (AMS) into your cluster, you should review Using Ambari Metrics in Hortonworks Data Platform Apache Ambari Operations, for guidelines on resources requirements. In general, the host you plan to run the Ambari Metrics Collector host should have the following memory and disk space available based on cluster size:

|---|---|---|
|Number of hosts|Memory Available|Disk Space|
|1|1024 MB|10 GB|
|10|1024 MB|20 GB|
|50|2048 MB|500 GB|
|100|4096 MB|100 GB|
|300|4096 MB|100 GB|
|500|8096 MB|200 GB|
|1000|12288 MB|200 GB|
|2000|16384 MB|500 GB|

> Use these values as guidelines. Be sure to test them for your specific environment.
