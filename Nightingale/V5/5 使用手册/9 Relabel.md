[TOC]

监控数据通过推模式，发给夜莺，夜莺会转发给后端时序库，有时候可能想对数据做一些二次处理，比如 Drop 掉一些数据或者改改内容之类的，此时就需要 relabel 能力了，这个功能是社区小伙伴贡献的，和 Prometheus 的 relabel 类似，只是配置的时候注意配置项的大小写。在夜莺 5.x 版本中，数据是通过 n9e-server 转发的，所以，relabel 的逻辑放在了 server.conf 中。

    [[Writers]]
    Url = "http://127.0.0.1:9090/api/v1/write"
    # Basic auth username
    BasicAuthUser = ""
    # Basic auth password
    BasicAuthPass = ""
    # timeout settings, unit: ms
    Headers = ["X-From", "n9e"]
    Timeout = 10000
    DialTimeout = 3000
    TLSHandshakeTimeout = 30000
    ExpectContinueTimeout = 1000
    IdleConnTimeout = 90000
    # time duration, unit: ms
    KeepAlive = 30000
    MaxConnsPerHost = 0
    MaxIdleConns = 100
    MaxIdleConnsPerHost = 100
    # [[Writers.WriteRelabels]]
    # Action = "replace"
    # SourceLabels = ["__address__"]
    # Regex = "([^:]+)(?::\\d+)?"
    # Replacement = "$1:80"
    # TargetLabel = "__address__"


relabel 的逻辑就是上面的 `[[Writers.WriteRelabels]]` 部分，双中括号的，所以这是个数组，每个 Writer 可以配置多个 Relabel 逻辑，Action 部分支持如下选项：

    const (
    	Replace   Action = "replace"
    	Keep      Action = "keep"
    	Drop      Action = "drop"
    	HashMod   Action = "hashmod"
    	LabelMap  Action = "labelmap"
    	LabelDrop Action = "labeldrop"
    	LabelKeep Action = "labelkeep"
    	Lowercase Action = "lowercase"
    	Uppercase Action = "uppercase"
    )


比如我想把带有 `env=test` 标签的数据删除，可以这么配置：

    [[Writers.WriteRelabels]]
    Action = "drop"
    SourceLabels = ["env"]
    Regex = "^test$"


其他的就不一一介绍了，大家知道这里支持 Relabel 这个功能就可以了，其他 Action 的用法可以参考 Prometheus 的文档。
