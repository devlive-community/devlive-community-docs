[TOC]

### Prerequisites

When using MySQL, the storage engine used for the Ranger admin policy store tables MUST support transactions. InnoDB is an example of engine that supports transactions. A storage engine that does not support transactions is not suitable as a policy store.

### Steps

If you are using Amazon RDS, see the [Amazon RDS Requirements]($MySQL_MariaDBPrerequisite).

1. The MySQL database administrator should be used to create the Ranger databases.

   The following series of commands could be used to create the `rangerdba` user with password `rangerdba`.

    a. Log in as the root user, then use the following commands to create the rangerdba user and grant it adequate privileges.

    ```sql
    CREATE USER 'rangerdba'@'localhost' IDENTIFIED BY 'rangerdba';
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'localhost';
    
    CREATE USER 'rangerdba'@'%' IDENTIFIED BY 'rangerdba';
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'%';
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'localhost' WITH GRANT OPTION;
    
    GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'%' WITH GRANT OPTION;
    
    FLUSH PRIVILEGES;
    ```
   
    b. Use the `exit` command to exit MySQL.

    c. You should now be able to reconnect to the database as `rangerdba` using the following command:

    ```bash
    mysql -u rangerdba -prangerdba 
    ```
    
    After testing the `rangerdba` login, use the `exit` command to exit MySQL.

2. Use the following command to confirm that the `mysql-connector-java.jar` file is in the Java share directory. This command must be run on the server where Ambari server is installed.

    ```bash
    ls /usr/share/java/mysql-connector-java.jar
    ```
    
    If the file is not in the Java share directory, use the following command to install the MySQL connector .jar file.
    
    #### RHEL/CentOS/Oracle/Aamazon Linux
    
    ```bash
    yum install mysql-connector-java*
    ```
    
    #### SLES
    
    ```bash
    zypper install mysql-connector-java*
    ```

3. Use the following command format to set the `jdbc/driver/path` based on the location of the MySQL JDBC driver .jar file.This command must be run on the server where Ambari server is installed.

    ```bash
    ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}
    ```
    
    For example:
    
    ```bash
    ambari-server setup --jdbc-db=mysql --jdbc-driver=/usr/share/java/mysql-connector-java.jar
    ```
