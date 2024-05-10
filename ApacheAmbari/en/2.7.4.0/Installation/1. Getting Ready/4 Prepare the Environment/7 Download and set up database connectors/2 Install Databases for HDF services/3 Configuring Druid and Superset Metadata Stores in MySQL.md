[TOC]

### About This Task

Druid and Superset require a relational data store to store metadata. To use MySQL for this, install MySQL and create a database for the Druid metastore.

### Steps

1. Launch the MySQL monitor:

    ```bash
    mysql -u root -p
    ```

2. Create the database for the Druid and Superset metastore:

    ```bash
    CREATE DATABASE druid DEFAULT CHARACTER SET utf8;
    CREATE DATABASE superset DEFAULT CHARACTER SET utf8;
    ```

3. Create druid and superset user accounts, replacing the final IDENTIFIED BY string with your password:

    ```bash
    CREATE USER 'druid'@'%' IDENTIFIED BY '9oNio)ex1ndL';
    CREATE USER 'superset'@'%' IDENTIFIED BY '9oNio)ex1ndL';
    ```

4. Assign privileges to the druid account:

    ```bash
    GRANT ALL PRIVILEGES ON *.* TO 'druid'@'%' WITH GRANT OPTION;
    GRANT ALL PRIVILEGES ON *.* TO 'superset'@'%' WITH GRANT OPTION;
    ```

5. Commit the operation:

    ```bash
    commit;
    ```
