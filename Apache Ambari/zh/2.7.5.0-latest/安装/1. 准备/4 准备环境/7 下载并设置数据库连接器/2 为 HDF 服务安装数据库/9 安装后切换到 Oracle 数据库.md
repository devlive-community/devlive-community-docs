[TOC]

### 关于此任务

如果在执行初始 HDF 安装或升级后想要将 Oracle 数据库与 SAM 或架构注册表一起使用，则可以切换到 Oracle 数据库。支持 Oracle 数据库 12c 和 11g 第 2 版

### 条件

您已安装并配置了 Oracle 数据库。

### 步骤

1. 登录 Ambari Server 并关闭 SAM 或架构注册表。
2. 从配置屏幕中，选择 Oracle 作为数据库类型，并提供 Oracle 凭据、JDBC 连接字符串，然后单击 **Save**。
3. 从运行 Ambari Server 的命令行中，注册 Oracle JDBC 驱动程序 jar：

    ```bash
    sudo ambari-server setup --jdbc-db=oracle --jdbc-driver=/usr/share/java/ojdbc.jar
    ```

4. 从安装 SAM 或架构注册表的主机中，将 JDBC jar 复制到以下位置，具体取决于您要更新的组件。

    ```bash
    cp ojdbc6.jar /usr/hdf/current/registry/bootstrap/lib/.
    cp ojdbc6.jar /usr/hdf/current/streamline/bootstrap/lib/.
    ```

5. 从安装 SAM 或架构注册表的主机上，运行以下命令来创建 SAM 或架构注册表所需的架构。

    ```bash
    export JAVA_HOME=/usr/jdk64/jdk1.8.0_112 ; source /usr/hdf/current/streamline/conf/streamline-env.sh ; /usr/hdf/current/streamline/bootstrap/bootstrap-storage.sh create
    
    export JAVA_HOME=/usr/jdk64/jdk1.8.0_112 ; source /usr/hdf/current/registry/conf/registry-env.sh ; /usr/hdf/current/registry/bootstrap/bootstrap-storage.sh create
    ```

    > 您只需从单个主机运行此命令一次即可准备数据库。

6. 确认 Oracle 数据库中已创建新表。
7. 从 Ambari 中，重新启动 SAM 或架构注册表。
8. 如果您为 SAM 指定 Oracle 数据库，请在重新启动 SAM 后运行以下命令。

    ```bash
    export JAVA_HOME=/usr/jdk64/jdk1.8.0_112 ; source /usr/hdf/current/streamline/conf/streamline-env.sh ; /usr/hdf/current/streamline/bootstrap/bootstrap.sh
    ```

9. 确认 Sam 或架构注册表可用并关闭维护模式。
