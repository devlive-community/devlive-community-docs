[TOC]

基本介绍
----

Categraf 是一款 all-in-one 的采集器，由 [快猫团队](https://flashcat.cloud/) 开源，代码托管在：

*   github: [https://github.com/flashcatcloud/categraf](https://github.com/flashcatcloud/categraf)

Categraf 不但可以采集 OS、MySQL、Redis、Oracle 等常见的监控对象，也准备提供日志采集能力和 trace 接收能力，这是夜莺主推的采集器，相关信息请查阅项目 [README](https://github.com/flashcatcloud/categraf/blob/main/README.md)

Categraf 采集到数据之后，通过 remote write 协议推给远端存储，Nightingale 恰恰提供了 remote write 协议的数据接收接口，所以二者可以整合在一起，重点是配置 Categraf 的 `conf/config.toml` 中的 writer 部分，其中 url 部分配置为 n9e-server 的 remote write 接口：

    [writer_opt]
    # default: 2000
    batch = 2000
    # channel(as queue) size
    chan_size = 10000
    
    [[writers]]
    url = "http://N9E-SERVER:19000/prometheus/v1/write"
    
    # Basic auth username
    basic_auth_user = ""
    
    # Basic auth password
    basic_auth_pass = ""
    
    # timeout settings, unit: ms
    timeout = 5000
    dial_timeout = 2500
    max_idle_conns_per_host = 100


采集插件
----

Categraf 每个采集器，都有一个配置目录，在 conf 下面，以 `input.` 打头，如果某个插件不想启用，就把插件配置目录改个名字，别让它是 `input.` 打头即可，比如 docker 不想采集，可以 `mv input.docker bak.input.docker` 就可以了。当然了，也并不是说只要有 input.xx 目录，就会采集对应的内容，比如 MySQL 监控插件，如果想采集其数据，至少要在 `conf/input.mysql/mysql.toml` 中配置要采集的数据库实例的连接地址。

每个采集插件的配置文件，都给了很详尽的注释，阅读这些注释，基本就了解如何去配置各个插件了。另外，有些采集插件还会同步提供夜莺监控大盘JSON和告警规则JSON，大家可以直接导入使用，在[代码的 inputs 目录](https://github.com/flashcatcloud/categraf/tree/main/inputs)，机器的监控大盘比较特殊，放到了 system 目录，没有分散在 cpu、mem、disk 等目录。

很多采集插件的配置文件中，都有 `[[instances]]` 配置段，这个 `[[]]` 在 toml 配置中表示数组，即 instances 配置段可以配置多份，比如 oracle 的配置文件：

    # collect interval, unit: second
    interval = 15
    
    [[instances]]
    address = "10.1.2.3:1521/orcl"
    username = "monitor"
    password = "123456"
    is_sys_dba = false
    is_sys_oper = false
    disable_connection_pool = false
    max_open_connections = 5
    # interval = global.interval * interval_times
    interval_times = 1
    labels = { region="cloud" }
    
    [[instances]]
    address = "192.168.10.10:1521/orcl"
    username = "monitor"
    password = "123456"
    is_sys_dba = false
    is_sys_oper = false
    disable_connection_pool = false
    max_open_connections = 5
    labels = { region="local" }


address 可以指定连接地址，如果想监控多个 oracle 实例，一个 address 显然不行了，就要把 instances 部分拷贝多份，即可做到监控多个 oracle 实例的效果。

当然，更多信息请查阅[Categraf README](https://github.com/flashcatcloud/categraf/blob/main/README.md)，README 中有 FAQ 和 QuickStart 的链接，可以帮助大家快速入门。另外，大家也可以参考我的公众号文章《[讲解Categraf采集器](https://mp.weixin.qq.com/s/T69kkBzToHVh31D87xsrIg)》里边有3个视频教程介绍Categraf，公众号也欢迎大家关注，会持续更新监控相关的文章。

