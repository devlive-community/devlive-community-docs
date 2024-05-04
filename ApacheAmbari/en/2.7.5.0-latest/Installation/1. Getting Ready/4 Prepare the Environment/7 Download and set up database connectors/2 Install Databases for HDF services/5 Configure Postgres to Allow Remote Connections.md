[TOC]

### About This Task

It is critical that you configure Postgres to allow remote connections before you deploy a cluster. If you do not perform these steps in advance of installing your cluster, the installation fails.

### Steps

1. Open `/var/lib/pgsql/9.6/data/pg_hba.conf` and update to the following

    ```bash
    # "local" is for Unix domain socket connections only
    local all all trust
    
    
    # IPv4 local connections:
    host all all 0.0.0.0/0 trust
    
    
    # IPv6 local connections:
    host all all ::/0 trust
    ```

2. Open `/var/lib//pgsql/9.6/data/postgresql.conf` and update to the following:

    ```bash
    listen_addresses = '*'
    ```

3. Restart Postgres:

    ```bash
    systemctl stop postgresql-9.6.service
    systemctl start postgresql-9.6.service 
    ```
