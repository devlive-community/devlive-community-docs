[TOC]

### 关于此任务

如果您已经安装了 MySQL 并使用 MySQL 配置了 SAM 和架构注册表元数据存储，则无需在 Postgres 中配置其他元数据存储。

### 步骤

1. 登录Postgres：
    
    ```bash
    sudo su postgres
    psql
    ```

2. 创建一个名为 `registry` 的数据库，密码为 `registry`：

    ```sql
    create database registry;
    CREATE USER registry WITH PASSWORD 'registry';
    GRANT ALL PRIVILEGES ON DATABASE "registry" to registry;
    ```

3. 创建一个名为 `streamline` 的数据库，密码为 `streamline`：

    ```sql
    create database streamline;
    CREATE USER streamline WITH PASSWORD 'streamline';
    GRANT ALL PRIVILEGES ON DATABASE "streamline" to streamline;
    ```
