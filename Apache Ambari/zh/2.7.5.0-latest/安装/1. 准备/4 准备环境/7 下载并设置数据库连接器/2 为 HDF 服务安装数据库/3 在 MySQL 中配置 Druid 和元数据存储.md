[TOC]

### 关于此任务

Druid 和 Superset 需要一个关系数据存储来存储元数据。要为此使用 MySQL，请安装 MySQL 并为 Druid 元存储创建数据库。

### 步骤

- 启动 MySQL 监视器：

    ```bash
    mysql -u root -p
    ```

- 为 Druid 和 Superset 元存储创建数据库：

    ```sql
    CREATE DATABASE druid DEFAULT CHARACTER SET utf8;
    CREATE DATABASE superset DEFAULT CHARACTER SET utf8;
    ```

- 创建 `druid` 和 `superset` 用户帐户，用您的密码替换最终的 `IDENTIFIED BY` 字符串：

    ```sql
    CREATE USER 'druid'@'%' IDENTIFIED BY '9oNio)ex1ndL';
    CREATE USER 'superset'@'%' IDENTIFIED BY '9oNio)ex1ndL';
    ```

- 为 `druid` 帐户分配权限：

    ```sql
    GRANT ALL PRIVILEGES ON *.* TO 'druid'@'%' WITH GRANT OPTION;
    GRANT ALL PRIVILEGES ON *.* TO 'superset'@'%' WITH GRANT OPTION;
    ```

- 提交操作：

    ```sql
    commit;
    ```
