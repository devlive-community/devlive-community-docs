[TOC]

### About This Task

Druid and Superset require a relational data store to store metadata. To use Postgres for this, install Postgres and create a database for the Druid metastore. If you have already created a data store using MySQL, you do not need to configure additional metadata stores in Postgres.

### Steps

1. Log in to Postgres:

    ```bash
    sudo su postgres
    psql
    ```
   
2. Create a database, user, and password, each called `druid`, and assign database privileges to the user `druid`:

    ```bash
    create database druid;
    CREATE USER 'druid' WITH PASSWORD 'druid';
    GRANT ALL PRIVILEGES ON DATABASE "druid" to druid;
    ```
   
3. Create a database, user, and password, each called `superset`, and assign database privileges to the user `superset`:

    ```bash
    create database superset;
    CREATE USER 'superset' WITH PASSWORD 'superset';
    GRANT ALL PRIVILEGES ON DATABASE "superset" to superset;
    ```

