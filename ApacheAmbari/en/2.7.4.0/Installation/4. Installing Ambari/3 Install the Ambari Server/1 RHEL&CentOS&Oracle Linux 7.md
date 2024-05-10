[TOC]

On a server host that has Internet access, use a command line editor to perform the following

### Steps

1. Install the Ambari bits. This also installs the default PostgreSQL Ambari database.
    
    ```bash
    yum install ambari-server
    ```

2. Enter `y` when prompted to confirm transaction and dependency checks.

    A successful installation displays output similar to the following:
    
    ```bash
   Installing : postgresql-libs-9.2.18-1.el7.x86_64         1/4
   Installing : postgresql-9.2.18-1.el7.x86_64              2/4
   Installing : postgresql-server-9.2.18-1.el7.x86_64       3/4
   Installing : ambari-server-2.7.4.0-118.x86_64           4/4
   Verifying  : ambari-server-2.7.4.0-118.x86_64           1/4
   Verifying  : postgresql-9.2.18-1.el7.x86_64              2/4
   Verifying  : postgresql-server-9.2.18-1.el7.x86_64       3/4
   Verifying  : postgresql-libs-9.2.18-1.el7.x86_64         4/4
   
   Installed:
   ambari-server.x86_64 0:2.7.4.0-118
   Dependency Installed:
   postgresql.x86_64 0:9.2.18-1.el7
   postgresql-libs.x86_64 0:9.2.18-1.el7
   postgresql-server.x86_64 0:9.2.18-1.el7
   Complete!
    ```
    
    > Accept the warning about trusting the Hortonworks GPG Key. That key will be automatically downloaded and used to validate packages from Hortonworks. You will see the following message:
    
    ```bash
    Importing GPG key 0x07513CAD: Userid: "Jenkins (HDP Builds) https://archive.cloudera.com/p/ambari/2.x/2.7.4.0/centos7/RPM-GPG-KEY/
   ```
   
    > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
    
    > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
