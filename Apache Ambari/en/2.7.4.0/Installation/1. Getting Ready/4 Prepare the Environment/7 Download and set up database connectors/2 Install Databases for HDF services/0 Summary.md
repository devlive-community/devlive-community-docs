[TOC]

When installing Schema Registry, SAM, Druid, and Superset, you require a relational data store to store metadata. You can use either MySQL, Postgres, Oracle, or MariaDB. These topics describe how to install MySQL, Postgres, and Oracle and how create a databases for SAM and Schema Registry. If you are installing on an existing HDP cluster by using Superset, you can skip the installation instructions, because MySQL was installed with Druid. In this case, configure the databases.

> You should install either Postgres, Oracle or MySQL; both are not necessary. It is recommended that you use MySQL.
> 
> If you are installing Postgres, you must install Postgres 9.5 or later for SAM and Schema Registry. Ambari does not install Postgres 9.5, so you must perform a manual Postgres installation.

### Installing and Configuring MySQL

- [Installing MySQL]($InstallingMySQL)
- [Configuring SAM and Schema Registry Metadata Stores in MySQL]($ConfiguringSAMAndSchemaRegistryMetadataStoreMySQL)
- [Configuring Druid and Superset Metadata Stores in MySQL]($ConfiguringDruidAndSupersetMetadataStoresInMySQL)

### Installing and Configuring Postgres

- [Install Postgres]($InstallingPostgres)
- [Configure Postgres to Allow Remote Connections]($ConfigurePostgresToAllowRemoteConnections)
- [Configure SAM and Schema Registry Metadata Stores in Postgres]($ConfiguringSAMAndSchemaRegistryMetadataStorePostgr)
- [Configure Druid and Superset Metadata Stores in Postgres]($ConfiguringDruidAndSupersetMetadataStoresInPostgre)

### Using an Oracle Database

- [the section called “Specifying an Oracle Database to Use with SAM and Schema Registry”]($SpecifyingAnOracleDatabaseToUseWithSAMAndSchemaReg)
- [the section called “Switching to an Oracle Database After Installation”]($SwitchingToAnOracleDatabaseAfterInstallation)
