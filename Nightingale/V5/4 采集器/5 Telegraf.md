[TOC]

Telegraf 是 InfluxData 公司开源的一款采集器，内置非常多的采集插件，不过 Telegraf 是面向 InfluxDB 生态的，采集的监控数据推给 InfluxDB 非常合适，推给 Prometheus、Victoriametrics、Thanos 这些时序库，可能会带来问题。主要是两点：

*   有些数据是 string 类型的，Prometheus、VM、M3、Thanos 等都不支持 string 类型的数据
*   有些采集器设计的标签是非稳态的设计，比如经常会看到 `result=success` 和 `result=failed` 的标签，需要手工配置采集器 drop 掉，但是对于新手确实有些难度

另外一个问题是，Telegraf 采集的数据存到 Prometheus 中，这种做法在业界实践的比较少，导致 Grafana 大盘很少，需要我们付出较大精力手工制作大盘。不过，如果，你是资深监控玩家，Telegraf 上面这些问题都不是问题。下面是笔者之前调研 Telegraf 的几篇笔记，供大家参考：

*   [Telegraf监控客户端调研笔记（1）-介绍、安装、初步测试](https://mp.weixin.qq.com/s/JeBa_YOJdsv_QOlCVDHdtw)
*   [Telegraf监控客户端调研笔记（2）-CPU、MEM、DISK、IO相关指标采集](https://mp.weixin.qq.com/s/alvO9k73wGHJFy5XjvMMsQ)
*   [Telegraf监控客户端调研笔记（3）-kernel、system、processes相关指标采集](https://mp.weixin.qq.com/s/PRZ_1EWD25QVuHKPvhD0oQ)
*   [Telegraf监控客户端调研笔记（4）-exec、net、netstat相关指标采集](https://mp.weixin.qq.com/s/bd3ml0KgWzfQVhYP162htQ)
*   [Telegraf监控客户端调研笔记（5）-本地端口监控&远程TCP探测](https://mp.weixin.qq.com/s/3z7rDNMZ-Gmub0fox0iMYg)
*   [Telegraf监控客户端调研笔记（6）-PING监控、进程监控](https://mp.weixin.qq.com/s/QJOaETU7r1silkj5RwuZbw)

Telegraf 是如何与 Nightingale 整合的呢？Telegraf 有不同的 output plugin，可以把采集的数据推给 OpenTSDB、推给 Datadog，Nightingale 实现了 OpenTSDB 和 Datadog 这两种消息接收接口，所以，可以通过任一 output plugin 和 Nightingale 对接。下面提供一个简单的 Telegraf 配置供大家参考，使用 OpenTSDB 的 output plugin 和 Nightingale 对接，即 `[[outputs.opentsdb]]` 配置段，host 部分配置为 n9e-server 的地址：

    #!/bin/sh
    
    version=1.20.4
    tarball=telegraf-${version}_linux_amd64.tar.gz
    wget https://dl.influxdata.com/telegraf/releases/$tarball
    tar xzvf $tarball
    
    mkdir -p /opt/telegraf
    cp -far telegraf-${version}/usr/bin/telegraf /opt/telegraf
    
    cat <<EOF > /opt/telegraf/telegraf.conf
    [global_tags]
    
    [agent]
      interval = "10s"
      round_interval = true
      metric_batch_size = 1000
      metric_buffer_limit = 10000
      collection_jitter = "0s"
      flush_interval = "10s"
      flush_jitter = "0s"
      precision = ""
      hostname = ""
      omit_hostname = false
    
    [[outputs.opentsdb]]
      host = "http://127.0.0.1"
      port = 19000
      http_batch_size = 50
      http_path = "/opentsdb/put"
      debug = false
      separator = "_"
    
    [[inputs.cpu]]
      percpu = true
      totalcpu = true
      collect_cpu_time = false
      report_active = true
    
    [[inputs.disk]]
      ignore_fs = ["tmpfs", "devtmpfs", "devfs", "iso9660", "overlay", "aufs", "squashfs"]
    
    [[inputs.diskio]]
    
    [[inputs.kernel]]
    
    [[inputs.mem]]
    
    [[inputs.processes]]
    
    [[inputs.system]]
      fielddrop = ["uptime_format"]
    
    [[inputs.net]]
      ignore_protocol_stats = true
    
    EOF
    
    cat <<EOF > /etc/systemd/system/telegraf.service
    [Unit]
    Description="telegraf"
    After=network.target
    
    [Service]
    Type=simple
    
    ExecStart=/opt/telegraf/telegraf --config telegraf.conf
    WorkingDirectory=/opt/telegraf
    
    SuccessExitStatus=0
    LimitNOFILE=65535
    StandardOutput=syslog
    StandardError=syslog
    SyslogIdentifier=telegraf
    KillMode=process
    KillSignal=SIGQUIT
    TimeoutStopSec=5
    Restart=always
    
    
    [Install]
    WantedBy=multi-user.target
    EOF
    
    systemctl daemon-reload
    systemctl enable telegraf
    systemctl restart telegraf
    systemctl status telegraf

