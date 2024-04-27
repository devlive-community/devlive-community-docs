由于 [Amazon RDS 的限制](https://forums.aws.amazon.com/thread.jspa?messageID=450535)，必须手动创建 Ranger 数据库用户和表空间，并且必须手动向 Ranger 数据库用户授予所需的权限。

1. 使用主用户帐号（创建 RDS Oracle实例时创建的）登录 RDS Oracle 服务器，执行以下命令：

    ```sql
    create user $rangerdbuser identified by “password”;
    GRANT CREATE SESSION,CREATE PROCEDURE,CREATE TABLE,CREATE VIEW,CREATE SEQUENCE,CREATE PUBLIC SYNONYM,CREATE ANY SYNONYM,CREATE TRIGGER,UNLIMITED Tablespace TO $rangerdbuser;
    create tablespace $rangerdb datafile size 10M autoextend on;
    alter user $rangerdbuser DEFAULT Tablespace $rangerdb;
    ```

    其中 `$rangerdb` 是实际的 Ranger 数据库名称（例如：ranger），`$rangerdbuser` 是 Ranger 数据库用户名（例如：rangeradmin）。

2. 如果您使用 Ranger KMS，请执行以下命令：

    ```sql
    create user $rangerdbuser identified by “password”;
    GRANT CREATE SESSION,CREATE PROCEDURE,CREATE TABLE,CREATE VIEW,CREATE SEQUENCE,CREATE PUBLIC SYNONYM,CREATE ANY SYNONYM,CREATE TRIGGER,UNLIMITED Tablespace TO $rangerkmsuser;
    create tablespace $rangerkmsdb datafile size 10M autoextend on;
    alter user $rangerkmsuser DEFAULT Tablespace $rangerkmsdb;
    ```

    其中 `$rangerkmsdb` 是实际的 Ranger 数据库名称（例如：rangerkms），`$rangerkmsuser` 是 Ranger 数据库用户名（例如：rangerkms）。
