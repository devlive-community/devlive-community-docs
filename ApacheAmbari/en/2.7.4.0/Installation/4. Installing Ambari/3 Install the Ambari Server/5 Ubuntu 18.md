[TOC]

On a server host that has Internet access, use a command line editor to perform the following

### Steps

1. Install the Ambari bits. This also installs the default PostgreSQL Ambari database.

   ```bash
    apt-get install ambari-server
    ```

    > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
    
    > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
