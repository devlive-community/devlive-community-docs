[TOC]

### Before You Begin

If you have already installed a MySQL database, you may skip these steps.

> You must install Postgres 9.5 or later for SAM and Schema Registry. Ambari does not install Postgres 9.5, so you must perform a manual Postgres installation.

### Steps

1. Install Red Hat Package Manager (RPM) according to the requirements of your operating system:

    ```bash
    yum install https://yum.postgresql.org/9.6/redhat/rhel-7-x86_64/pgdg-redhat96-9.6-3.noarch.rpm
    ```

2. Install Postgres version 9.5 or later:
    
    ```bash
    yum install postgresql96-server postgresql96-contrib postgresql96
    ```

3. Initialize the database:

    - For CentOS 7, use the following syntax:

    ```bash
    /usr/pgsql-9.6/bin/postgresql96-setup initdb
    ```

   - For CentOS 6, use the following syntax:

    ```bash
    sudo service postgresql initdb
    ```

4. Start Postgres.

   For example, if you are using CentOS 7, use the following syntax:

    ```bash
    systemctl enable postgresql-9.6.service
    systemctl start postgresql-9.6.service
    ```

5. Verify that you can log in:

    ```bash
    sudo su postgres
    psql
    ```
