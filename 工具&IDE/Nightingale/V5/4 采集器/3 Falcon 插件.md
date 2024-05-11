[TOC]

Nightingale 实现了 Open-Falcon 的 HTTP 数据接收接口，所以，Open-Falcon 社区很多采集插件也是可以直接使用的。但是 Falcon-Agent 不行，因为 Falcon-Agent 推送监控数据给服务端，走的是 RPC 接口。

如果你发现某个 Falcon-Plugin 是用 CRON 的方式驱动的，推送数据走的是 Falcon-Agent 的 HTTP 接口，那这个插件就可以推数据给夜莺。举个例子，比如 [mymon](https://github.com/open-falcon/mymon) 其配置文件采用 ini 格式，下面是样例：

    [default]
    basedir = . # 工作目录
    log_dir = ./fixtures # 日志目录，默认日志文件为myMon.log,旧版本有log_file项，如果同时设置了，会优先采用log_file
    ignore_file = ./falconignore # 配置忽略的metric项
    snapshot_dir = ./snapshot # 保存快照(process, innodb status)的目录
    snapshot_day = 10 # 保存快照的时间(日)
    log_level  = 5 #  日志级别[RFC5424]
    # 0 LevelEmergency
    # 1 LevelAlert
    # 2 LevelCritical
    # 3 LevelError
    # 4 LevelWarning
    # 5 LevelNotice
    # 6 LevelInformational
    # 7 LevelDebug
    falcon_client=http://127.0.0.1:1988/v1/push # falcon agent连接地址
    
    [mysql]
    user=root # 数据库用户名
    password=1tIsB1g3rt # 您的数据库密码
    host=127.0.0.1 # 数据库连接地址
    port=3306 # 数据库端口


注意 falcon\_client 配置项，配置的是 Falcon-Agent 的数据接收接口，可以把这个配置改成夜莺 n9e-server 的地址： `http://N9E-SERVER:19000/openfalcon/push` 。

Open-Falcon 的监控数据中有一个 endpoint 字段，夜莺会把 endpoint 字段当做监控对象唯一标识来对待，自动解析之后入库，就可以在对象列表中看到了。当然，如果没有 endpoint 字段也没关系，使用 metric 和 tags 也是可以唯一标识一个 Series 的。

