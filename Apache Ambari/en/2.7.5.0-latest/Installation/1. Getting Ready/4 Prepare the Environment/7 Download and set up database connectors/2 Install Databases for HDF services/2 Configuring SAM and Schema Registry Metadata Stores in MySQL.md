[TOC]

### Steps

1. Launch the MySQL monitor:

    ```bash
    mysql -u root -p
    ```

2. Create the database for Schema Registry and SAM metastore:

    ```sql
    create database registry;
    create database streamline;
    ```

3. Create Schema Registry and SAM user accounts, replacing the final IDENTIFIED BY string with your password:

    ```sql
    CREATE USER 'registry'@'%' IDENTIFIED BY 'R12$%34qw';
    CREATE USER 'streamline'@'%' IDENTIFIED BY 'R12$%34qw';
    ```
   
4. Assign privileges to the user account:

    ```sql
    GRANT ALL PRIVILEGES ON registry.* TO 'registry'@'%' WITH GRANT OPTION ;
    GRANT ALL PRIVILEGES ON streamline.* TO 'streamline'@'%' WITH GRANT OPTION ;
    ```

5. Commit the operation:
    
    ```sql
    commit;
    ```
