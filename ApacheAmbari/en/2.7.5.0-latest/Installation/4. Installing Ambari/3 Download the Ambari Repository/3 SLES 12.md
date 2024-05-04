[TOC]

On a server host that has Internet access, use a command line editor to perform the following:

### Steps

1. Log in to your host as `root`.
2. Download the Ambari repository file to a directory on your installation host.

    ```bash
    wget -nv https://username:password@archive.cloudera.com/p/ambari/sles12/2.x/updates/2.7.5.0/ambari.repo -O /etc/zypp/repos.d/ambari.repo
    ```
    
    > Do not modify the `ambari.repo` file name. This file is expected to be available on the Ambari Server host during Agent registration.

3. Confirm the downloaded repository is configured by checking the repo list.

    ```bash
    zypper repos
    ```

    You should see the Ambari repositories in the list.

    ```bash
    # | Alias                    | Name                                 | Enabled | Refresh
    --+------------------------- +--------------------------------------+---------+--------
    1 | ambari-2.7.5.0-72      | ambari Version - ambari-2.7.5.0-72 | Yes     | No
    2 | http-demeter.uni         | SUSE-Linux-Enterprise-Software
         -regensburg.de-c997c8f9 |  -Development-Kit-12-SP1 12.1.1-1.57 | Yes     | Yes
    3 | opensuse                 | OpenSuse                             | Yes     | Yes
    ```

    Version values vary, depending on the installation.
    
    > When deploying a cluster having limited or no Internet access, you should provide access to the bits using an alternative method.
    
    > Ambari Server by default uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for install. These packages are typically available as part of your Operating System repositories. Please confirm you have the appropriate repositories available for the postgresql-server packages.

### Next Step

- [Install the Ambari Server]($InstallTheAmbariServer)
- [Set Up the Ambari Server]($SetUpTheAmbariServer)

### More Information

- [Using a Local Repository]($UsingALocalRepository)
