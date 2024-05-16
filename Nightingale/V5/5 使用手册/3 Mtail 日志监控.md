[TOC]

前言
--

说到日志监控，大家第一反应的可能是ELK的方案，或者Loki的方案，这两个方案都是把日志采集了发到中心，在中心存储、查看、分析，不过这个方案相对比较重量级一些，如果我们的需求只是从日志中提取一些metrics数据，比如统计一些日志中出现的Error次数之类的，则有一个更简单的方案。

这里给大家介绍一个Google出品的小工具，[mtail](https://github.com/google/mtail)，mtail就是流式读取日志，通过正则表达式匹配的方式从日志中提取metrics指标，这种方式可以利用目标机器的算力，不过如果量太大，可能会影响目标机器上的业务程序，另外一个好处是无侵入性，不需要业务埋点，如果业务程序是第三方供应商提供的，我们改不了其代码，mtail此时就非常合适了。当然了，如果业务程序是我们公司的人自己写的，那还是建议用埋点的方式采集指标，mtail只是作为一个补充吧。

更新
--

从 Categraf v0.2.17 开始，我们把 mtail 整合到了 Categraf 中，可以少部署一堆进程了，详情参考：《[从应用日志中提取监控metrics](https://flashcat.cloud/blog/log-monitoring-mtail/)》，这个文章博客的内容已经非常详细，本节文档后面的内容理论上不用看了。

mtail简介
-------

mtail的使用方案，参考如下两个文档（下载的话参考[Releases](https://github.com/google/mtail/releases)页面）：

*   [Deploying](https://github.com/google/mtail/blob/main/docs/Deploying.md)
*   [Programming Guide](https://google.github.io/mtail/Programming-Guide.html)

我们拿mtail的启动命令来举例其用法：

    mtail --progs /etc/mtail --logs /var/log/syslog --logs /var/log/ntp/peerstats


通过 `--progs` 参数指定一个目录，这个目录里放置一堆的`*.mtail`文件，每个mtail文件就是描述的正则提取规则，通过 `--logs` 参数来指定要监控的日志目录，可以写通配符，`--logs` 可以写多次，上例中只是指定了 `--progs` 和 `--logs` ，没有其他参数，mtail启动之后会自动监听一个端口3903，在3903的`/metrics`接口暴露符合Prometheus协议的监控数据，Prometheus 或者 Categraf 或者 Telegraf 等就可以从 `/metrics` 接口提取监控数据。

这样看起来，原理就很清晰了，mtail 启动之后，根据 `--logs` 找到相关日志文件，seek 到文件末尾，开始流式读取，每读到一行，就根据 `--progs` 指定的那些规则文件做匹配，看是否符合某些正则，从中提取时序数据，然后通过3903的`/metrics`暴露采集到的监控指标。当然，除了Prometheus这种`/metrics`方式暴露，mtail 还支持把监控数据直接推给 graphite 或者 statsd，具体可以参考：[这里](https://github.com/google/mtail/blob/main/docs/Interoperability.md)

mtail样例
-------

这里我用mtail监控一下n9e-server的日志，从中提取一下各个告警规则触发的 notify 的数量，这个日志举例：

    2021-12-27 10:00:30.537582 INFO engine/logger.go:19 event(cbb8d4be5efd07983c296aaa4dec5737 triggered) notify: rule_id=9 [__name__=net_response_result_code author=qin ident=10-255-0-34 port=4567 protocol=tcp server=localhost]2@1640570430


很明显，日志中有这么个关键字：`notify: rule_id=9`，可以用正则来匹配，统计出现的行数，ruleid 也可以从中提取到，这样，我们可以把 ruleid 作为标签上报，于是乎，我们就可以写出这样的 mtail 规则了：

    [root@10-255-0-34 nightingale]# cat /etc/mtail/n9e-server.mtail
    counter mtail_alert_rule_notify_total by ruleid
    
    /notify: rule_id=(?P<ruleid>\d+)/ {
        mtail_alert_rule_notify_total[$ruleid]++
    }


然后启动也比较简单，我这里就用 nohup 简单来做：

    nohup mtail -logtostderr --progs /etc/mtail --logs server.log &> stdout.log &


mtail 没有指定绝对路径，是因为我把 mtail 的二进制直接放在了 `/usr/bin` 下面了，mtail 默认会监听在 3903，所以我们可以用如下命令验证：

    curl -s localhost:3903/metrics
    # output:
    # HELP mtail_alert_rule_notify_total defined at n9e-server.mtail:1:9-37
    # TYPE mtail_alert_rule_notify_total counter
    mtail_alert_rule_notify_total{prog="n9e-server.mtail",ruleid="9"} 6


上面的输出只是挑选了部分内容，没有全部贴出，这就表示正常采集到了，如果 n9e 的 server.log 中当前没有打印 notify 相关的日志，那请求`/metrics`接口是没法得到上面的输出的，可以手工配置一条必然会触发的规则，待日志里有相关输出的时候再次请求 `/metrics` 接口，应该就有了。

最后我们在 Categraf （或者 Telegraf） 中配置一下抓取规则，抓取本机的 `http://localhost:3903/metrics` 即可，然后重启 Categraf，等一会就可以在页面查到相关指标了。

另外，mtail 的配置文件如果发生变化，是需要重启 mtail 才能生效的，或者发一个 SIGHUP 信号给 mtail，mtail 收到信号就会重新加载配置。

mtail更多样例
---------

mtail 的 github repo 中有一个 [examples](https://github.com/google/mtail/tree/main/examples)，里边有挺多例子，大家可以参考。我在这里再给大家举一个简单例子，比如我们要统计 /var/log/messages 文件中的 `Out of memory` 关键字，mtail 规则应该怎么写呢？其实比上面举例的 mtail\_alert\_rule\_notify\_total 还要更简单：

    counter mtail_oom_total
    
    /Out of memory/ {
        mtail_oom_total++
    }


关于时间戳
-----

最后说一下时间戳的问题，日志中每一行一般都是有个时间戳的，夜莺v4版本在页面上配置采集规则的时候，就是要选择时间戳的，但是 mtail，上面的例子中没有处理时间戳，为啥？其实 mtail 也可以支持从日志中提取时间戳，如果没有配置的话，就用系统当前时间，个人认为，用系统当前时间就可以了，从日志中提取时间稍微还有点麻烦，当然，系统当前时间和日志中的时间可能稍微有差别，但是不会差很多的，可以接受，examples 中的 mtail 样例，也基本都没有给出时间戳的提取。
