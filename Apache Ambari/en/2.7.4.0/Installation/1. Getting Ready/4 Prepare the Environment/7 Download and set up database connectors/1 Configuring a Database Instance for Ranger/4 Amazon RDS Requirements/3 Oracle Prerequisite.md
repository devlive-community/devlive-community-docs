[TOC]

Due to [limitations in Amazon RDS](https://forums.aws.amazon.com/thread.jspa?messageID=450535), the Ranger database user and tablespace must be created manually and the required privileges must be manually granted to the Ranger database user.

1. Log in to the RDS Oracle Server from the master user account (created during RDS Oracle instance creation) and execute following commands:

    ```sql
    create user $rangerdbuser identified by “password”;
    GRANT CREATE SESSION,CREATE PROCEDURE,CREATE TABLE,CREATE VIEW,CREATE SEQUENCE,CREATE PUBLIC SYNONYM,CREATE ANY SYNONYM,CREATE TRIGGER,UNLIMITED Tablespace TO $rangerdbuser;
    create tablespace $rangerdb datafile size 10M autoextend on;
    alter user $rangerdbuser DEFAULT Tablespace $rangerdb;
    ```
    
    Where `$rangerdb` is a actual Ranger database name (for example: ranger) and `$rangerdbuser` is Ranger database username (for example: rangeradmin).

2. If you are using Ranger KMS, execute the following commands:

    ```sql
    create user $rangerdbuser identified by “password”;
    GRANT CREATE SESSION,CREATE PROCEDURE,CREATE TABLE,CREATE VIEW,CREATE SEQUENCE,CREATE PUBLIC SYNONYM,CREATE ANY SYNONYM,CREATE TRIGGER,UNLIMITED Tablespace TO $rangerkmsuser;
    create tablespace $rangerkmsdb datafile size 10M autoextend on;
    alter user $rangerkmsuser DEFAULT Tablespace $rangerkmsdb;
    ```
    
    Where `$rangerkmsdb` is a actual Ranger database name (for example: rangerkms) and `$rangerkmsuser` is Ranger database username (for example: rangerkms).
