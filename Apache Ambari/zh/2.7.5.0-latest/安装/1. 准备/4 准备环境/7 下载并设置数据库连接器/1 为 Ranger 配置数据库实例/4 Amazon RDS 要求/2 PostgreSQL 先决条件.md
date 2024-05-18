Amazon RDS PostgreSQL Server 中的 Ranger 数据库用户应在安装 Ranger 之前创建，并且应被授予必须具有 CREATEDB 角色的现有角色。

1. 使用主用户账户，从主用户账户（在创建 RDS PostgreSQL 实例期间创建）登录 Amazon RDS PostgreSQL 服务器并执行以下命令：

    a. `CREATE USER $rangerdbuser WITH LOGIN PASSWORD 'password'`

    b. `GRANT $rangerdbuser to $postgresroot`

    其中 `$postgresroot` 是 RDS PostgreSQL 主用户帐户（例如：postgresroot），`$rangerdbuser` 是 Ranger 数据库用户名（例如：rangeradmin）。

2. 如果您使用 Ranger KMS，请执行以下命令：

    a. `CREATE USER $rangerkmsuser WITH LOGIN PASSWORD 'password'`

    b. `GRANT $rangerkmsuser to $postgresroot`

    其中 `$postgresroot` 是 RDS PostgreSQL 主用户帐户（例如：postgresroot），`$rangerkmsuser` 是 Ranger KMS 用户名（例如：rangerkms）。
