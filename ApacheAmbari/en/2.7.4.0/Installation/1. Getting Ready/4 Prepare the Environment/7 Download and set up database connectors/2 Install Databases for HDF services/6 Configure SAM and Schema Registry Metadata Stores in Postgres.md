[TOC]

### About This Task

If you have already installed MySQL and configured SAM and Schema Registry metadata stores using MySQL, you do not need to configure additional metadata stores in Postgres.

### Steps

1. Log in to Postgres:

    ```bash
    sudo su postgres
    psql
    ```

2. Create a database called `registry` with the password `registry`:

    ```bash
    create database registry;
    CREATE USER registry WITH PASSWORD 'registry';
    GRANT ALL PRIVILEGES ON DATABASE "registry" to registry;
    ```

3. Create a database called `streamline` with the password `streamline`:
    
    ```bash
    create database streamline;
    CREATE USER streamline WITH PASSWORD 'streamline';
    GRANT ALL PRIVILEGES ON DATABASE "streamline" to streamline;
    ```
