[TOC]

### 关于此任务

Druid 和 Superset 需要一个关系数据存储来存储元数据。要为此使用 Postgres，请安装 Postgres 并为 Druid 元存储创建数据库。如果您已经使用 MySQL 创建了数据存储，则无需在 Postgres 中配置其他元数据存储。

### 步骤

1. 登录 Postgres：

    ```bash
    sudo su postgres
    psql
    ```

2. 创建数据库、用户和密码，分别称为 `druid`，并为用户 `druid` 分配数据库权限：

    ```sql
    create database druid;
    CREATE USER druid WITH PASSWORD 'druid';
    GRANT ALL PRIVILEGES ON DATABASE  "druid" to druid;
    ```

3. 创建一个数据库、用户和密码，每个都称为 `superset`，并将数据库权限分配给用户 `superset`：

    ```sql
    create database superset;
    CREATE USER superset WITH PASSWORD 'superset';
    GRANT ALL PRIVILEGES ON DATABASE "superset" to superset;
    ```
