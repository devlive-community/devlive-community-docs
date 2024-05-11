[TOC]

Grafana-agent 是 Grafana 开源的一款 Agent，专门用于和自己的 Cloud 做数据采集集成，通过 remote write 协议推数据给后端，和 Categraf 的数据推送方式一样，所以，也是可以作为 Nightingale 的采集器的。Grafana-Agent 的具体使用请查阅 Grafana 官方文档，下面给出 v0.23.0 版本的 Grafana-Agent 的简要安装方式，如果各位看官使用了其他版本的 Grafana-Agent，下面的教程可能就不适用了，毕竟，Grafana-Agent 也在快速迭代，请大家注意。

1\. 下载二进制
---------

以 64 位 Linux 举例：

    curl -SOL "https://github.com/grafana/agent/releases/download/v0.23.0/agent-linux-amd64.zip"
    gunzip ./agent-linux-amd64.zip
    chmod a+x "agent-linux-amd64"


2\. 生成配置
--------

    cat <<EOF > ./agent-cfg.yaml
    server:
      log_level: info
      http_listen_port: 12345
    
    metrics:
      global:
        scrape_interval: 15s
        scrape_timeout: 10s
        remote_write:
          - url: https://N9E-SERVER:19000/prometheus/v1/write
            basic_auth:
              username: ""
              password: ""
    
    integrations:
      agent:
        enabled: true
    
      node_exporter:
        enabled: true
        include_exporter_metrics: true
    EOF


上面的 url 部分，就是 n9e-server 的 remote write 数据接收接口，仔细看就会发现，和 Categraf 章节用的 url 是一样的。

3\. 启动 grafana-agent
--------------------

    nohup ./agent-linux-amd64 \
      -config.file ./agent-cfg.yaml \
      -metrics.wal-directory ./data \
      &> grafana-agent.log &


上面的配置内置启用了 node\_exporter，Grafana-Agent 内置了很多 exporter，省的到处去找 exporter 了.

