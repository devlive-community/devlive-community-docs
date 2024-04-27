[TOC]

### 在你开始之前

如果您已经安装了MySQL数据库，则可以跳过这些步骤。

> 您必须为 SAM 和架构注册表安装 Postgres 9.5 或更高版本。 Ambari 不安装 Postgres 9.5，因此您必须执行手动 Postgres 安装。

### 步骤

1. 根据操作系统的要求安装 Red Hat Package Manager (RPM)：

    ```bash
    yum install https://yum.postgresql.org/9.6/redhat/rhel-7-x86_64/pgdg-redhat96-9.6-3.noarch.rpm
    ```

2. 安装 Postgres 9.5 或更高版本：

    ```bash
    yum install postgresql96-server postgresql96-contrib postgresql96
    ```

3. 初始化数据库：

    - 对于 CentOS 7，请使用以下语法：

        ```bash
        /usr/pgsql-9.6/bin/postgresql96-setup initdb
        ```

    - 对于 CentOS 6，请使用以下语法：

        ```bash
        sudo service postgresql initdb
        ```
   
4. 启动 Postgres。

    例如，如果您使用的是 CentOS 7，请使用以下语法：
    
    ```bash
    systemctl enable postgresql-9.6.service
    systemctl start postgresql-9.6.service 
    ```

5. 验证您是否可以登录：
    
    ```bash
    sudo su postgres
    psql
    ```
