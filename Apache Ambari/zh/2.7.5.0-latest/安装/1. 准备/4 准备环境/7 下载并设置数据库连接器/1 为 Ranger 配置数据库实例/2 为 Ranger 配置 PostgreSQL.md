如果您使用 Amazon RDS，请参阅 [Amazon RDS 要求]($PostgreSQLPrerequisite)。

1. 在 PostgreSQL 主机上，安装适用的 PostgreSQL 连接器。

    #### RHEL/CentOS/Oracle/Aamazon Linux

    ```bash
    yum install postgresql-jdbc*
    ```
   
    #### SLES

    ```bash
    zypper install -y postgresql-jdbc
    ```
   
2. 确认 .jar 文件位于 Java 共享目录中。

    ```bash
    ls /usr/share/java/postgresql-jdbc.jar
    ```
3. 将 jar 文件的访问模式修改为 644。

    ```bash
    chmod 644 /usr/share/java/postgresql-jdbc.jar
    ```

4. 应使用 PostgreSQL 数据库管理员来创建 Ranger 数据库。

    以下一系列命令可用于创建 `rangerdba` 用户并授予其足够的权限。

    ```sql
    echo "CREATE DATABASE $dbname;" | sudo -u $postgres psql -U postgres
    echo "CREATE USER $rangerdba WITH PASSWORD '$passwd';" | sudo -u $postgres psql -U postgres
    echo "GRANT ALL PRIVILEGES ON DATABASE $dbname TO $rangerdba;" | sudo -u $postgres psql -U postgres
    ```

   在命令里：

   - `$postgres` 是 Postgres 用户。

   - `$dbname` 是你的 PostgreSQL 数据库的名称

5. 使用以下命令格式根据 PostgreSQL JDBC 驱动程序 .jar 文件的位置设置 `jdbc/driver/path`。该命令必须在安装了 Ambari 服务器的服务器上运行。

    ```bash
    ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}
    ```

    示例

    ```bash
    ambari-server setup --jdbc-db=postgres --jdbc-driver=/usr/share/java/postgresql-jdbc.jar
    ```

6. 运行以下命令：

    ```bash
    export HADOOP_CLASSPATH=${HADOOP_CLASSPATH}:${JAVA_JDBC_LIBS}:/connector jar path
    ```

7. 添加 Ranger 用户的允许访问详细信息：

    - 将 `listen_addresses='localhost'` 更改为 `listen_addresses='*' ('*' = any)` 以监听 `postgresql.conf` 中的所有IP。
    - 对 `pg_hba.conf` 文件中的 Ranger db 用户和 Rangeraudit db 用户进行以下更改。
    ![img.png](https://docs.cloudera.com/HDPDocuments/Ambari-2.7.5.0/bk_ambari-installation/content/figures/1/figures/installing_ranger_postgres_changes.png)

8. 编辑 `pg_hba.conf` 文件后，运行以下命令刷新 PostgreSQL 数据库配置：

    ```bash
    sudo -u postgres /usr/bin/pg_ctl -D $PGDATA reload
    ```

    例如，如果 `pg_hba.conf` 文件位于 `/var/lib/pgsql/data` 目录中，则 `$PGDATA` 的值为 `/var/lib/pgsql/data`。
