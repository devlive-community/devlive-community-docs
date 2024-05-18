[TOC]

On a server host that has Internet access, use a command line editor to perform the following

### Steps

1. Log in to your host as `root`.
2. Download the Ambari repository file to a directory on your installation host.

    ```bash
    wget -nv https://archive.cloudera.com/p/ambari/2.x/2.7.4.0/centos7/ambari.repo -O /etc/yum.repos.d/ambari.repo   
    ```
    
    > Do not modify the `ambari.repo` file name. This file is expected to be available on the Ambari Server host during Agent registration.

3. Confirm that the repository is configured by checking the repo list.

   ```bash
   yum repolist
   ```

   You should see values similar to the following for Ambari repositories in the list.
   
   ```bash
   repo id                    repo name                                       status
   ambari-2.7.4.0-118        ambari Version - ambari-2.7.4.0-118            12
   epel/x86_64                Extra Packages for Enterprise Linux 7 - x86_64  11,387
   ol7_UEKR4/x86_64           Latest Unbreakable Enterprise Kernel Release 4
   for Oracle Linux 7Server (x86_64)   295
   ol7_latest/x86_64          Oracle Linux 7Server Latest (x86_64)            18,642
   puppetlabs-deps/x86_64     Puppet Labs Dependencies El 7 - x86_64          17
   puppetlabs-products/x86_64 Puppet Labs Products El 7 - x86_64              225
   repolist: 30,578
   ```
   
   Version values vary, depending on the installation.
   
   > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
   > 
   > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Install the Ambari Server]($InstallTheAmbariServer)
- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
