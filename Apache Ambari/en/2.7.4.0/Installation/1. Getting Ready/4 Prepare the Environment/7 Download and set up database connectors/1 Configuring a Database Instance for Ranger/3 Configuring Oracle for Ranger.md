[TOC]

If you are using Amazon RDS, see the [Amazon RDS Requirements]($OraclePrerequisite).

1. On the Oracle host, install the appropriate JDBC .jar file.

   - Download the Oracle JDBC (OJDBC) driver from http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html.
   - For `Oracle Database 11g`: select Oracle Database 11g Release 2 drivers > ojdbc6.jar.
   - For `Oracle Database 12c`: select Oracle Database 12c Release 1 driver > ojdbc7.jar.
   - Copy the .jar file to the Java share directory. For example:

       ```bash
       cp ojdbc7.jar /usr/share/java/
       ```
    
       > Make sure the .jar file has the appropriate permissions. For example:
    
       ```bash
       chmod 644 /usr/share/java/ojdbc7.jar
       ```

2. The Oracle database administrator should be used to create the Ranger databases. The following series of commands could be used to create the `RANGERDBA` user and grant it permissions using SQL*Plus, the Oracle database administration utility:

   ```sql
   # sqlplus sys/root as sysdba
   CREATE USER $RANGERDBA IDENTIFIED BY $RANGERDBAPASSWORD;
   GRANT SELECT_CATALOG_ROLE TO $RANGERDBA;
   GRANT CONNECT, RESOURCE TO $RANGERDBA;
   QUIT;
   ```

3. Use the following command format to set the `jdbc/driver/path` based on the location of the Oracle JDBC driver .jar file. This command must be run on the server where Ambari server is installed.

    ```bash
    ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}
    ```
    
    For example:
    
    ```bash
    ambari-server setup --jdbc-db=oracle --jdbc-driver=/usr/share/java/ojdbc6.jar
    ```
