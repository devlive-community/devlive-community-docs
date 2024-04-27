如果您使用 Amazon RDS，请参阅 [Amazon RDS 要求]($OraclePrerequisite)。

1. 在 Oracle 主机上，安装适当的 JDBC .jar 文件。

    - 从 [http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html) 下载 Oracle JDBC (OJDBC) 驱动程序。
    - `Oracle Database 11g`：选择 Oracle Database 11g 第 2 版驱动程序 > ojdbc6.jar。
    - `Oracle Database 12c`：选择 Oracle Database 12c 第 1 版驱动程序 > ojdbc7.jar。
    - 将 .jar 文件复制到 Java 共享目录。例如：

        `cp ojdbc7.jar /usr/share/java/`
    
        > 确保 .jar 文件具有适当的权限。例如：
    
        > `chmod 644 /usr/share/java/ojdbc7.jar`

2. 应使用 Oracle 数据库管理员来创建 Ranger 数据库。

    以下一系列命令可用于创建 `RANGEDBA` 用户并使用 SQL*Plus（Oracle 数据库管理实用程序）授予其权限：

    ```sql
    # sqlplus sys/root as sysdba
    CREATE USER $RANGERDBA IDENTIFIED BY $RANGERDBAPASSWORD;
    GRANT SELECT_CATALOG_ROLE TO $RANGERDBA;
    GRANT CONNECT, RESOURCE TO $RANGERDBA;
    QUIT;
    ```

3. 使用以下命令格式根据 Oracle JDBC 驱动程序 .jar 文件的位置设置 `jdbc/driver/path`。该命令必须在安装了 Ambari 服务器的服务器上运行。

    ```bash
    ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}
    ```

    示例

    ```bash
    ambari-server setup --jdbc-db=oracle --jdbc-driver=/usr/share/java/ojdbc6.jar
    ```
