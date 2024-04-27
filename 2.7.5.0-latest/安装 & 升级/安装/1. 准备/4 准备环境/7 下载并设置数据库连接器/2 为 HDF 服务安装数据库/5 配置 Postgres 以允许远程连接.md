[TOC]

### 关于此任务

在部署集群之前，将 Postgres 配置为允许远程连接至关重要。如果您在安装集群之前未执行这些步骤，安装将失败。

### 步骤

1. 打开 `/var/lib/pgsql/9.6/data/pg_hba.conf` 并更新为以下内容

    ```bash
    # "local" is for Unix domain socket connections only
    local all all trust
    
    
    # IPv4 local connections:
    host all all 0.0.0.0/0 trust
    
    
    # IPv6 local connections:
    host all all ::/0 trust
    ```

2. 打开 `/var/lib//pgsql/9.6/data/postgresql.conf` 并更新为以下内容：

    ```bash
    listen_addresses = '*'
    ```

3. 重新启动Postgres：

    ```bash
    systemctl stop postgresql-9.6.service
    systemctl start postgresql-9.6.service 
    ```
