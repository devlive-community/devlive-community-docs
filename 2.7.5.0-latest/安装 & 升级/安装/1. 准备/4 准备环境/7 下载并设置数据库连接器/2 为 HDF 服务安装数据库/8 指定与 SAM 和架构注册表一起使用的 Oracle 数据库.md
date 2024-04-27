[TOC]

### 关于此任务

您可以使用具有 SAM 和架构注册表的 Oracle 数据库。支持 Oracle 数据库 12c 和 11g 第 2 版

### 条件

您已安装并配置了 Oracle 数据库。

### 步骤

1. 注册 Oracle JDBC 驱动程序 jar。

    ```bash
    sudo ambari-server setup --jdbc-db=oracle --jdbc-driver=/usr/share/java/ojdbc.jar
    ```

2. 从 SAM 架构注册表配置屏幕中，选择 Oracle 作为数据库类型，并提供必要的 Oracle Server JDBC 凭据和连接字符串。
