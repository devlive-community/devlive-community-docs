[TOC]

## Command Entrypoint

> Spark 2

```bash
bin/start-seatunnel-spark-2-connector-v2.sh
```

> Spark 3

```bash
bin/start-seatunnel-spark-3-connector-v2.sh
```

> Flink 13 14

```bash
bin/start-seatunnel-flink-13-connector-v2.sh
```

> Flink 15 16

```bash
bin/start-seatunnel-flink-15-connector-v2.sh
```

## Options

> Spark 2

```bash
Usage: start-seatunnel-spark-2-connector-v2.sh [options]
  Options:
    --check           Whether check config (default: false)
    -c, --config      Config file
    -e, --deploy-mode Spark deploy mode, support [cluster, client] (default: 
                      client) 
    -h, --help        Show the usage message
    -m, --master      Spark master, support [spark://host:port, 
                      mesos://host:port, yarn, k8s://https://host:port, 
                      local], default local[*] (default: local[*])
    -n, --name        SeaTunnel job name (default: SeaTunnel)
    -i, --variable    Variable substitution, such as -i city=beijing, or -i 
                      date=20190318 (default: [])
```

> Spark 3

```bash
Usage: start-seatunnel-spark-3-connector-v2.sh [options]
  Options:
    --check           Whether check config (default: false)
    -c, --config      Config file
    -e, --deploy-mode Spark deploy mode, support [cluster, client] (default: 
                      client) 
    -h, --help        Show the usage message
    -m, --master      Spark master, support [spark://host:port, 
                      mesos://host:port, yarn, k8s://https://host:port, 
                      local], default local[*] (default: local[*])
    -n, --name        SeaTunnel job name (default: SeaTunnel)
    -i, --variable    Variable substitution, such as -i city=beijing, or -i 
                      date=20190318 (default: [])
```

> Flink 13 14

```bash
Usage: start-seatunnel-flink-13-connector-v2.sh [options]
  Options:
    --check            Whether check config (default: false)
    -c, --config       Config file
    -e, --deploy-mode  Flink job deploy mode, support [run, run-application] 
                       (default: run)
    -h, --help         Show the usage message
    --master, --target Flink job submitted target master, support [local, 
                       remote, yarn-session, yarn-per-job, kubernetes-session, 
                       yarn-application, kubernetes-application]
    -n, --name         SeaTunnel job name (default: SeaTunnel)
    -i, --variable     Variable substitution, such as -i city=beijing, or -i 
                       date=20190318 (default: [])
```

> Flink 15 16

```bash
Usage: start-seatunnel-flink-15-connector-v2.sh [options]
  Options:
    --check            Whether check config (default: false)
    -c, --config       Config file
    -e, --deploy-mode  Flink job deploy mode, support [run, run-application] 
                       (default: run)
    -h, --help         Show the usage message
    --master, --target Flink job submitted target master, support [local, 
                       remote, yarn-session, yarn-per-job, kubernetes-session, 
                       yarn-application, kubernetes-application]
    -n, --name         SeaTunnel job name (default: SeaTunnel)
    -i, --variable     Variable substitution, such as -i city=beijing, or -i 
                       date=20190318 (default: [])
```

## Example

> Spark 2

```bash
bin/start-seatunnel-spark-2-connector-v2.sh --config config/v2.batch.config.template -m local -e client
```

> Spark 3

```bash
bin/start-seatunnel-spark-3-connector-v2.sh --config config/v2.batch.config.template -m local -e client
```

> Flink 13 14

```bash
bin/start-seatunnel-flink-13-connector-v2.sh --config config/v2.batch.config.template
```

> Flink 15 16

```bash
bin/start-seatunnel-flink-15-connector-v2.sh --config config/v2.batch.config.template
```
