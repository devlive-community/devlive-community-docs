### 先决条件

使用 MySQL 时，用于 Ranger 管理策略存储表的存储引擎必须支持事务。 InnoDB 是支持事务的引擎的一个例子。不支持事务的存储引擎不适合作为策略存储。

### 操作步骤

如果您使用 Amazon RDS，请参阅 [Amazon RDS 要求](https://docs.devlive.org/read/apache-ambari-installation-2.7.5.0/MySQL_MariaDBPrerequisite)。

1. 应使用 MySQL 数据库管理员来创建 Ranger 数据库。

   以下一系列命令可用于创建带有密码 `rangerdba` 的 `rangerdba` 用户。

   a. 以 `root` 用户身份登录，然后使用以下命令创建 `rangerdba` 用户并授予其足够的权限。

   ```sql
    CREATE USER 'rangerdba'@'localhost' IDENTIFIED BY 'rangerdba';

    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'localhost';
    
    CREATE USER 'rangerdba'@'%' IDENTIFIED BY 'rangerdba';
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'%';
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'localhost' WITH GRANT OPTION;
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'%' WITH GRANT OPTION;
    
    FLUSH PRIVILEGES;
   ```
   
   b. 使用 `exit` 命令退出 MySQL。

   c. 您现在应该能够使用以下命令以 `rangerdba` 身份重新连接到数据库：

   ```sql
   mysql -u rangerdba -prangerdba
   ```

   测试 `rangerdba` 登录后，使用 `exit` 命令退出 MySQL。


2. 使用以下命令确认 `mysql-connector-java.jar` 文件位于 Java 共享目录中。该命令必须在安装了 Ambari 服务器的服务器上运行。

   ```bash
   ls /usr/share/java/mysql-connector-java.jar 
   ```

    如果该文件不在 Java 共享目录中，请使用以下命令安装 MySQL 连接器 .jar 文件。

    ##### RHEL/CentOS/Oracle/Aamazon Linux

    ```bash
    yum install mysql-connector-java*
    ```
   
    ##### SLES

    ```bash
    zypper install mysql-connector-java*
    ```

3. 使用以下命令格式根据 MySQL JDBC 驱动程序 .jar 文件的位置设置 `jdbc/driver/path`。该命令必须在安装 Ambari 服务器的服务器上运行。

    ```bash
    ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}
    ```
    
    示例
    
    ```bash
    ambari-server setup --jdbc-db=mysql --jdbc-driver=/usr/share/java/mysql-connector-java.jar
    ```
