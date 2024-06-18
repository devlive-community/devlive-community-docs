[TOC]

# Run Job With Local Mode

Only for test.

The most recommended way to use SeaTunnel Engine in the production environment is [Cluster Mode]($cluster-mode).

## Deploy SeaTunnel Engine Local Mode

[Deploy a SeaTunnel Engine Local Mode reference]($Deployment)

## Change SeaTunnel Engine Config

Update the auto-increment to true in the $SEATUNNEL_HOME/config/hazelcast.yaml

## Submit Job

```shell
$SEATUNNEL_HOME/bin/seatunnel.sh --config $SEATUNNEL_HOME/config/v2.batch.config.template -e local
```

