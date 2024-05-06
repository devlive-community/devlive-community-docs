[TOC]

On a server host that has Internet access, use a command line editor to perform the following:

### Steps

1. Log in to your host as `root`.
2. Download the Ambari list file to a directory on your installation host.

    ```bash
    wget -O /etc/apt/sources.list.d/ambari.list https://username:password@archive.cloudera.com/p/ambari/ubuntu16/2.x/updates/2.7.5.0/ambari.list
    ```
   
   ```bash
   apt-key adv --recv-keys --keyserver keyserver.ubuntu.com B9733A7A07513CAD
   ```
   
   ```bash
   apt-get update
   ```
    
   > Do not modify the `ambari.list` file name. This file is expected to be available on the Ambari Server host during Agent registration.

3. Confirm that Ambari packages downloaded successfully by checking the package name list.

    ```bash
    apt-cache showpkg ambari-server
    ```
   
    ```bash
    apt-cache showpkg ambari-agent
    ```
   
    ```bash
    apt-cache showpkg ambari-metrics-assembly
    ```

    You should see the Ambari packages in the list.

    > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
    
    > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Install the Ambari Server]($InstallTheAmbariServer)
- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
