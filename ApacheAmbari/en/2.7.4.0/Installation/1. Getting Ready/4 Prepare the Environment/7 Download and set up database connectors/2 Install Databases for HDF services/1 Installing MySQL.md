[TOC]

### About This Task

You can install MySQL 5.5 or later.

### Before You Begin

On the Ambari host, install the JDBC driver for MySQL, and then add it to Ambari:

```bash
yum install mysql-connector-java* \
sudo ambari-server setup --jdbc-db=mysql \
--jdbc-driver=/usr/share/java/mysql-connector-java.jar
```

### Steps

1. Log in to the node on which you want to install the MySQL metastore to use for SAM, Schema Registry, and Druid.
2. Install MySQL and the MySQL community server, and start the MySQL service:

    ```bash
    yum localinstall \
    https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
    
    yum install mysql-community-server
    
    systemctl start mysqld.service
    ```

3. Obtain the randomly generated MySQL root password.

```bash
grep 'A temporary password is generated for root@localhost' \
/var/log/mysqld.log |tail -1
```

4. Reset the MySQL root password. Enter the following command. You are prompted for the password you obtained in the previous step. MySQL then asks you to change the password.

```bash
/usr/bin/mysql_secure_installation
```
