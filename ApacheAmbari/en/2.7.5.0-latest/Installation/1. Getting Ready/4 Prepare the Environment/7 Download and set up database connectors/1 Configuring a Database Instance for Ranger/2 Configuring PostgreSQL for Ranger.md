[TOC]

If you are using Amazon RDS, see the [Amazon RDS Requirements]($PostgreSQLPrerequisite).

1. On the PostgreSQL host, install the applicable PostgreSQL connector.

    #### RHEL/CentOS/Oracle/Aamazon Linux
    
    ```bash
    yum install postgresql-jdbc*
    ```
    
    #### SLES
    
    ```bash
    zypper install -y postgresql-jdbc
    ```

2. Confirm that the .jar file is in the Java share directory.
    
    ```bash
    ls /usr/share/java/postgresql-jdbc.jar
    ```

3. Change the access mode of the .jar file to 644.

    ```bash
    chmod 644 /usr/share/java/postgresql-jdbc.jar
    ```

4. The PostgreSQL database administrator should be used to create the Ranger databases.

    The following series of commands could be used to create the `rangerdba` user and grant it adequate privileges.
    
    ```sql
    echo "CREATE DATABASE $dbname;" | sudo -u $postgres psql -U postgres
    echo "CREATE USER $rangerdba WITH PASSWORD '$passwd';" | sudo -u $postgres psql -U postgres
    echo "GRANT ALL PRIVILEGES ON DATABASE $dbname TO $rangerdba;" | sudo -u $postgres psql -U postgres 
    ```

    Where:

    - `$postgres` is the Postgres user.

    - `$dbname` is the name of your PostgreSQL database

5. Use the following command format to set the `jdbc/driver/path` based on the location of the PostgreSQL JDBC driver .jar file. This command must be run on the server where Ambari server is installed.

    ```bash
    ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}
    ```
    
    For example:
    
    ```bash
    ambari-server setup --jdbc-db=postgres --jdbc-driver=/usr/share/java/postgresql-jdbc.jar
    ```

6. Run the following command:

    ```bash
    export HADOOP_CLASSPATH=${HADOOP_CLASSPATH}:${JAVA_JDBC_LIBS}:/connector jar path
    ```

7. Add Allow Access details for Ranger users:

   - change `listen_addresses='localhost'` to `listen_addresses='*' ('*' = any)` to listen from all IPs in `postgresql.conf`.
   - Make the following changes to the Ranger db user and Ranger audit db user in the `pg_hba.conf` file.
     ![img.png](https://docs.cloudera.com/HDPDocuments/Ambari-2.7.5.0/bk_ambari-installation/content/figures/1/figures/installing_ranger_postgres_changes.png)

8. After editing the `pg_hba.conf` file, run the following command to refresh the PostgreSQL database configuration:

    ```bash
    sudo -u postgres /usr/bin/pg_ctl -D $PGDATA reload
    ```
    
    For example, if the `pg_hba.conf` file is located in the `/var/lib/pgsql/data` directory, the value of `$PGDATA` is
    
    ```bash
    /var/lib/pgsql/data
    ```
