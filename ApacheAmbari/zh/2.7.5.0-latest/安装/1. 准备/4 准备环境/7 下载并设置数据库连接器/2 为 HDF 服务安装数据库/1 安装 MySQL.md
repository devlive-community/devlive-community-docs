[TOC]

### 关于此任务

您可以安装 MySQL 5.5 或更高版本。

### 在你开始之前

在 Ambari 主机上，安装 MySQL 的 JDBC 驱动程序，然后将其添加到 Ambari：

```bash
yum install mysql-connector-java* \
sudo ambari-server setup --jdbc-db=mysql \
--jdbc-driver=/usr/share/java/mysql-connector-java.jar
```

### 步骤

1. 登录到要安装 MySQL 元存储以用于 SAM、架构注册表和 Druid 的节点。
2. 安装MySQL和MySQL社区服务器，并启动MySQL服务：

    ```bash
    yum localinstall \
    https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
    
    yum install mysql-community-server
    
    systemctl start mysqld.service
    ```

3. 获取随机生成的 MySQL root 密码。

    ```bash
    grep 'A temporary password is generated for root@localhost' \
    /var/log/mysqld.log |tail -1
    ```

4. 重置 MySQL root 密码。输入以下命令。系统会提示您输入在上一步中获得的密码。然后 MySQL 会要求您更改密码。

    ```bash
    /usr/bin/mysql_secure_installation
    ```