[TOC]

On a server host that has Internet access, use a command line editor to perform the following

### Steps

1. Before installing Ambari, you must update `username` and `password` in the `ambari.repo` file. Run the following command: **vi /etc/zypp/repos.d/ambari.repo**

    For example, the output displays the following:
    
   ```bash
   [ambari-2.7.5.0]
   name=ambari Version - ambari-2.7.5.0
   enabled=1
   autorefresh=0
   username=<username>
   password=<password>
   baseurl=https://archive.cloudera.com/p/ambari/sles12/2.x/updates/2.7.5.0
   type=rpm-md
   priority=1
   gpgcheck=0
   gpgkey=https://archive.cloudera.com/p/ambari/sles12/2.x/updates/2.7.5.0/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
   ```

2. Next, install the Ambari bits. This also installs the default PostgreSQL Ambari database.

    ```bash
    zypper install ambari-server
    ```

3. Enter `y` when prompted to confirm transaction and dependency checks.

    A successful installation displays output similar to the following:
    
    ```bash
   Retrieving package postgresql-libs-8.3.5-1.12.x86_64 (1/4), 172.0 KiB (571.0 KiB unpacked)
   Retrieving: postgresql-libs-8.3.5-1.12.x86_64.rpm [done (47.3 KiB/s)]
   Installing: postgresql-libs-8.3.5-1.12 [done]
   Retrieving package postgresql-8.3.5-1.12.x86_64 (2/4), 1.0 MiB (4.2 MiB unpacked)
   Retrieving: postgresql-8.3.5-1.12.x86_64.rpm [done (148.8 KiB/s)]
   Installing: postgresql-8.3.5-1.12 [done]
   Retrieving package postgresql-server-8.3.5-1.12.x86_64 (3/4), 3.0 MiB (12.6 MiB unpacked)
   Retrieving: postgresql-server-8.3.5-1.12.x86_64.rpm [done (452.5 KiB/s)]
   Installing: postgresql-server-8.3.5-1.12 [done]
   Updating etc/sysconfig/postgresql...
   Retrieving package ambari-server-2.7.4.0-118.noarch (4/4), 99.0 MiB (126.3 MiB unpacked)
   Retrieving: ambari-server-2.7.4.0-118.noarch.rpm [done (3.0 MiB/s)]
   Installing: ambari-server-2.7.4.0-118 [done]
    ambari-server 0:off 1:off 2:off 3:on 4:off 5:on 6:off
    ```
    
    > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
    
    > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
