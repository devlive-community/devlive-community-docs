[TOC]

### About This Task

You may use an Oracle database with SAM and Schema Registry. Oracle databases 12c and 11g Release 2 are supported

### Prerequisites

You have an Oracle database installed and configured.

### Steps

1. Register the Oracle JDBC driver jar.

    ```bash
    sudo ambari-server setup --jdbc-db=oracle --jdbc-driver=/usr/share/java/ojdbc.jar
    ```
   
2. From the SAM an Schema Registry configuration screen, select Oracle as the database type and provide the necessary Oracle Server JDBC credentials and connection string.
