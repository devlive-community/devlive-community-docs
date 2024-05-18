[TOC]

### 步骤

- 启动 MySQL 监视器：

    ```bash
    mysql -u root -p
    ```

- 为架构注册表和 SAM 元存储创建数据库：

    ```sql
    create database registry;
    create database streamline;
    ```
  
- 创建架构注册表和 SAM 用户帐户，用您的密码替换最终的 IDENTIFIED BY 字符串：

    ```sql
    CREATE USER 'registry'@'%' IDENTIFIED BY 'R12$%34qw';
    CREATE USER 'streamline'@'%' IDENTIFIED BY 'R12$%34qw';
    ```
  
- 为用户帐户分配权限：

    ```sql
    GRANT ALL PRIVILEGES ON registry.* TO 'registry'@'%' WITH GRANT OPTION ;
    GRANT ALL PRIVILEGES ON streamline.* TO 'streamline'@'%' WITH GRANT OPTION ;
    ```

- 提交操作：

    ```sql
    commit;
    ```
