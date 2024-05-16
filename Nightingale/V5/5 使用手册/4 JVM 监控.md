[TOC]

本讲介绍JVM监控相关知识。

进程级监控
-----

Java类的程序，如果只是监控端口存活性，可以直接使用 Categraf 的 [net\_response](https://github.com/flashcatcloud/categraf/tree/main/inputs/net_response) 插件，如果只是监控进程存活性，以及进程的CPU、内存等使用率，这个和C的程序、Go的程序没有本质区别，使用 Categraf 的 [procstat](https://github.com/flashcatcloud/categraf/tree/main/inputs/procstat) 插件。

procstat 插件的采集配置文件中，有这么一段配置：

    # gather jvm metrics only when jstat is ready
    # gather_more_metrics = [
    #     "threads",
    #     "fd",
    #     "io",
    #     "uptime",
    #     "cpu",
    #     "mem",
    #     "limit",
    #     "jvm"
    # ]


如果打开，才能采集进程的 threads、fd、io、cpu、mem等的情况，如果不打开，只能采集到进程数量。其中 gather\_more\_metrics 中有一项是 jvm，如果配置了 jvm 这一项，会通过 jstat 采集一些 jvm 相关的指标，前提是机器上得有 jstat 命令可以用。

埋点方式
----

这个方式的监控，之前社区里有小伙伴分享过，链接在[这里](https://www.yuque.com/docs/share/67b03a91-5b83-4a4c-bc33-c7b970774b93)，这里就不重复讲解了


