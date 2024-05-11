[TOC]

Datadog 是专门提供监控和分析服务的 SaaS 服务商，市值几百亿，成立了10多年了，他们做的客户端采集器，理论上应该是比较完备的，夜莺实现了几个 Datadog 特定的接口，可以接收Datadog-Agent 推送上来的数据，即：我们可以拿 Datadog-Agent 作为客户端采集器采集监控数据，然后上报给夜莺。

1、注册datadog的账号
--------------

[https://www.datadoghq.com/](https://www.datadoghq.com/)

2、选择套餐
------

[https://app.datadoghq.com/billing/plan](https://app.datadoghq.com/billing/plan) 可以选择免费的套餐

3、拿到agent安装命令
-------------

[https://app.datadoghq.com/account/settings#agent](https://app.datadoghq.com/account/settings#agent) 选择对应的OS，比如CentOS7，可能是类似这么个命令：

    DD_AGENT_MAJOR_VERSION=7 DD_API_KEY=xxx DD_SITE="datadoghq.com" bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script.sh)"


DD\_API\_KEY 是一串字符串，不同的账号有自己的 API\_KEY，拿着这个命令去 shell 下（使用root账号应该会省事一些）跑一下安装

4、修改配置文件
--------

修改 Datadog-Agent 的配置文件，把推送监控数据的地址，改成 n9e-server 的地址，配置文件地址在：/etc/datadog-agent/datadog.yaml 修改 dd\_url 这个配置项，比如我的环境：

    dd_url: http://10.206.0.16:19000/datadog


5、重启datadog-agent
-----------------

    systemctl restart datadog-agent
