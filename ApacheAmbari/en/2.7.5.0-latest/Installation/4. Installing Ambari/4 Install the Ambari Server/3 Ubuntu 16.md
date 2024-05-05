[TOC]

On a server host that has Internet access, use a command line editor to perform the following

Before you install Ambari server, make sure to install the `apt-transport-https` package on all hosts as follows:

```bash
apt-get install apt-transport-https
```

### Steps

1. Before installing Ambari, you must update `username` and `password` in the `ambari.list` file. Run the following command: **vi /etc/apt/sources.list.d/ambari.list**

    For example, the output displays the following:
    
   ```bash
   #VERSION_NUMBER=2.7.5.0-72
   #json.url = https://archive.cloudera.com/p/ambari/2.7.5.0-72//ubuntu16/HDP/hdpdev_urlinfo.json
   deb https://username:password@archive.cloudera.com/p/ambari/2.7.5.0-72/ubuntu16 Ambari main
   ```

2. Next, install the Ambari bits. This also installs the default PostgreSQL Ambari database.

    ```bash
    apt-get install ambari-server
    ```

    > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
    
    > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
