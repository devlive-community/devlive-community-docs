[TOC]

The Ranger database user in Amazon RDS PostgreSQL Server should be created before installing Ranger and should be granted an existing role which must have the role CREATEDB.

1. Using the master user account, log in to the Amazon RDS PostgreSQL Server from master user account (created during RDS PostgreSQL instance creation) and execute following commands:

    a. `CREATE USER $rangerdbuser WITH LOGIN PASSWORD 'password'`

    b. `GRANT $rangerdbuser to $postgresroot`

    Where `$postgresroot` is the RDS PostgreSQL master user account (for example: postgresroot) and `$rangerdbuser` is the Ranger database user name (for example: rangeradmin).

2. If you are using Ranger KMS, execute the following commands:

    a. `CREATE USER $rangerkmsuser WITH LOGIN PASSWORD 'password'`

    b. `GRANT $rangerkmsuser to $postgresroot`
    
    Where `$postgresroot` is the RDS PostgreSQL master user account (for example: postgresroot) and `$rangerkmsuser` is the Ranger KMS user name (for example: rangerkms).
