[TOC]

简介
--

[VictoriaMetrics](https://github.com/VictoriaMetrics/VictoriaMetrics) 架构简单，可靠性高，在性能，成本，可扩展性方面表现出色，社区活跃，且和 Prometheus 生态绑定紧密。如果单机版本的 Prometheus 无法在容量上满足贵司的需求，可以使用 VictoriaMetrics 作为时序数据库。

VictoriaMetrics 提供[单机版](https://docs.victoriametrics.com/Single-server-VictoriaMetrics.html)和[集群版](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html)。如果您的每秒写入数据点数小于100万（这个数量是个什么概念呢，如果只是做机器设备的监控，每个机器差不多采集200个指标，采集频率是10秒的话每台机器每秒采集20个指标左右，100万/20=5万台机器），VictoriaMetrics 官方默认推荐您使用单机版，单机版可以通过增加服务器的CPU核心数，增加内存，增加IOPS来获得线性的性能提升。且单机版易于配置和运维。

集群架构
----

![Image 1](https://flashcat.cloud/images/docs/n9e/install/install-vm.png)

vmstorage、vminsert、vmselect 三者组合构成 VictoriaMetrics 的集群功能，三者都可以通过启动多个实例来分担承载流量，通过要在 vminsert 和 vmselect 前面架设负载均衡。

**vmstorage 是数据存储模块**

*   其数据保存在`-storageDataPath`指定的目录中，默认为`./vmstorage-data/`，vmstorage 是有状态模块，删除 storage node 会丢失约 `1/N`的历史数据（N 为集群中 vmstorage node 的节点数量）。增加 storage node，则需要同步修改 vminsert 和 vmselect 的启动参数，将新加入的storage node节点地址通过命令行参数 `-storageNode`传入给vminsert和vmselect
*   vmstorage 启动后，会监听三个端口，分别是 `-httpListenAddr :8482`、`-vminsertAddr :8400`、`-vmselectAddr :8401`。端口`8400`负责接收来自 vminsert 的写入请求，端口`8401`负责接收来自 vmselect 的数据查询请求，端口`8482`则是 vmstorage 自身提供的 http api 接口

**vminsert 接收来自客户端的数据写入请求，并负责转发到选定的vmstorage**

*   vminsert 接收到数据写入请求后，按照 [jump consistent hash](https://github.com/lithammer/go-jump-consistent-hash) 算法，将数据转发到选定的某个vmstorage node 上。vminsert 本身是无状态模块，可以增加或者删除一个或多个实例，而不会造成数据的损失。vminsert 模块通过启动时的参数 `-storageNode xxx,yyy,zzz` 来感知到整个 vmstorage 集群的完整 node 地址列表
*   vminsert 启动后，会监听一个端口`-httpListenAddr :8480`。该端口实现了 `prometheus remote_write`协议，因此可以接收和解析通过 `remote_write` 协议写入的数据。不过要注意，VictoriaMetrics 集群版本具有`多租户`功能，因此租户ID会以如下形式出现在 API URL 中: `http://vminsert:8480/insert/<account_id>/prometheus/api/v1/write`
*   更多 URL Format 可以参考 [VictoriaMetrics官网](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html#url-format)

**vmselect 接收来自客户端的数据查询请求，并负责转发到所有的 vmstorage 查询结果，最后将结果 merge 后返回**

*   vmselect 启动后，会监听一个端口`-httpListenAddr :8481`。该端口实现了 `prometheus query`相关的接口。不过要注意，VictoriaMetrics 集群版本具有`多租户`功能，因此租户ID会以如下形式出现在 API URL 中: `http://vminsert:8481/select/<account_id>/prometheus/api/v1/query`。
*   更多 URL Format 可以参考 [VictoriaMetrics官网](https://docs.victoriametrics.com/Cluster-VictoriaMetrics.html#url-format)

安装部署
----

1、 去 [vm release](https://github.com/VictoriaMetrics/VictoriaMetrics/releases) 下载编译好的二进制版本，比如我们选择下载 [v1.69.0 amd64](https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/v1.69.0/victoria-metrics-amd64-v1.69.0-cluster.tar.gz)。

2、 解压缩后得到：

    $ ls -l vm*-prod
    -rwxr-xr-x 1 work work 10946416 Nov  8 22:03 vminsert-prod*
    -rwxr-xr-x 1 work work 13000624 Nov  8 22:03 vmselect-prod*
    -rwxr-xr-x 1 work work 11476736 Nov  8 22:03 vmstorage-prod*


3、 启动三个 vmstorage 实例（可以用下面的脚本快速生成不同实例的启动命令）

    #!/bin/bash    
       
    for i in `seq 0 2`; do  
        if [ $i -eq 0 ]; then
            i=""   
        fi         
       
        pp=$i      
       
        httpListenAddr=${pp}8482
        vminsertAddr=${pp}8400
        vmselectAddr=${pp}8401
        storageDataPath=./${pp}vmstorage-data
       
        prog="nohup ./vmstorage-prod -loggerTimezone Asia/Shanghai \
            -storageDataPath $storageDataPath \
            -httpListenAddr :$httpListenAddr \
            -vminsertAddr :$vminsertAddr \
            -vmselectAddr :$vmselectAddr \
            &> ${pp}vmstor.log &"
       
        echo $prog 
        (exec "$prog")                                                                                                                   
    done


也可以输入以下命令行启动三个实例：

    nohup ./vmstorage-prod -loggerTimezone Asia/Shanghai -storageDataPath ./vmstorage-data -httpListenAddr :8482 -vminsertAddr :8400 -vmselectAddr :8401 &> vmstor.log &
    nohup ./vmstorage-prod -loggerTimezone Asia/Shanghai -storageDataPath ./1vmstorage-data -httpListenAddr :18482 -vminsertAddr :18400 -vmselectAddr :18401 &> 1vmstor.log &
    nohup ./vmstorage-prod -loggerTimezone Asia/Shanghai -storageDataPath ./2vmstorage-data -httpListenAddr :28482 -vminsertAddr :28400 -vmselectAddr :28401 &> 2vmstor.log &


4、 启动一个 vminsert 实例：

    nohup ./vminsert-prod -httpListenAddr :8480 -storageNode=127.0.0.1:8400,127.0.0.1:18400,127.0.0.1:28400 &>vminsert.log &


5、 启动一个 vmselect 实例：

    nohup ./vmselect-prod -httpListenAddr :8481 -storageNode=127.0.0.1:8401,127.0.0.1:18401,127.0.0.1:28401 &>vmselect.log &


6、 查看 vmstorage，vminsert，vmselect 的 /metrics 接口:

    curl http://127.0.0.1:8482/metrics 
    curl http://127.0.0.1:18482/metrics 
    curl http://127.0.0.1:28482/metrics 
    curl http://127.0.0.1:8481/metrics 
    curl http://127.0.0.1:8480/metrics 


7、 n9e-server 通过 remote write 协议写入时序库，VictoriaMetrics 作为时序库的一个选择，其 remote write 接口地址为：`http://127.0.0.1:8480/insert/0/prometheus/api/v1/write` 把这个地址配置到 server.conf 当中，配置完了重启 n9e-server

    # Reader部分修改Url
    [Reader]
    Url = "http://172.21.0.8:8481/select/0/prometheus"
    
    # Writers部分修改Url
    [[Writers]]
    Url = "http://172.21.0.8:8480/insert/0/prometheus/api/v1/write"


8、 修改 n9e-webapi 的配置文件 `./etc/webapi.conf` 如下：

    [[Clusters]]
    # Prometheus cluster name
    Name = "Default"
    # Prometheus APIs base url
    Prom = "http://127.0.0.1:8481/select/0/prometheus"


然后，重启 n9e-webapi，这样夜莺就可以查询到 VictoriaMetrics 集群的数据了。

如果您使用的是 VictoriaMetrics 单机版，端口是 8428，故而 Nightingale 的配置文件需要做如下调整：

    # server.conf
    # Reader部分修改为：
    [Reader]
    Url = "http://127.0.0.1:8428"
    
    # Writers部分修改为：
    [[Writers]]
    Url = "http://127.0.0.1:8428/api/v1/write"
    

    # webapi.conf
    # Clusters部分修改为：
    [[Clusters]]
    Name = "Default"
    Prom = "http://127.0.0.1:8428"


FAQ
---

**VictoriaMetrics 单机版本如何保障数据的可靠性？**

vm 针对磁盘IO有针对性的优化，单机版可以考虑将数据的可靠性保障交给 EBS 等云盘来保证。

**VictoriaMetrics 如何评估容量？**

参考vm的[官方文档](https://docs.victoriametrics.com/#capacity-planning)。

**VictoriaMetrics 集群版本增加或者删除 vmstorage node 的时候，数据如何再平衡？**

vm 不支持扩缩容节点时，对数据进行自动的再平衡。

**VictoriaMetrics 的数据大小如何查看？**

可以通过 vmstorage 实例暴露的 /metrics 接口来获取到相应的统计数据，譬如：

    $ curl http://127.0.0.1:8482/metrics |grep -i data_size
    vm_data_size_bytes{type="indexdb"} 609291
    vm_data_size_bytes{type="storage/big"} 0
    vm_data_size_bytes{type="storage/small"} 8749893


**vminsert 在将数据写入多个 vmstorage node的时候，是按照什么规则将数据写入到不同的 node 上的？**

采用 jump consistent hash 对数据进行分片，写入到相应的 storage node 上。

**vmselect 在接到查询请求的时候，如何定位到请求的数据是在哪个 storage node上的？**

vmselect 并不知道每个 metrics 对应的数据分布的 storage node，vmselect 会对所有的 storage node 发起查询请求，最后进行数据合并，并返回。

**VictoriaMetrics 和 M3db 的对比和选择？**

m3db 架构设计上更高级，实现难度高，m3db 在时序数据功能之后，重点解决了自动扩缩容，数据自动平衡等运维难题。但是因此也更复杂，可靠性也更难保证。VictoriaMetrics 架构设计上更倾向于简单可靠，重点优化了单机版的性能，强调垂直扩展，同时和 prometheus 生态做到兼容，甚至于在很多的点上做到了加强。但是 VictoriaMetrics 对于时序数据 downsample，节点的自动扩缩容，数据自动再平衡等高级功能和分布式能力，是有缺失的。

相关资料
----

*   [使用 Docker Compose 快速部署 VictoriaMetrics](https://docs.victoriametrics.com/Single-server-VictoriaMetrics.html#start-with-docker-compose)
*   [使用 Helm Chart 快速在 Kubernetes中部署 VictoriaMetrics](https://github.com/VictoriaMetrics/helm-charts)
*   [使用 VictoriaMetrics Operator 在 Kubernetes中部署 VictoriaMetrics](https://github.com/VictoriaMetrics/operator)

