[TOC]

### Steps

1. Download the `ambari.repo` file from the public repository:

    ```bash
    https://username:password@archive.cloudera.com/p/ambari/<OS>/2.x/updates/2.7.4.0/ambari.repo
    ```
    
    `<OS>` – centos7, sles12, ubuntu16, ubuntu 18, or debian9

2. Edit the `ambari.repo` file and replace the Ambari Base URL `baseurl` obtained when setting up your local repository.

    ```bash
   #VERSION_NUMBER=2.7.4.0
   [ambari-2.7.4.0]
   name=ambari Version - ambari-2.7.4.0
   baseurl=https://username:password@archive.cloudera.com/p/ambari/2.x/2.7.4.0/centos7
   gpgcheck=1
   gpgkey=https://archive.cloudera.com/p/ambari/2.x/2.7.4.0/centos7/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
   enabled=1
   priority=1
    ```

    > You can disable the GPG check by setting gpgcheck =0. Alternatively, you can keep the check enabled but replace gpgkey with the URL to GPG-KEY in your local repository.

    #### Base URL for a Local Repository
    
    **Built with Repository Tarball (No Internet Access)**
    
    ```bash
    http://<web.server>/Ambari-2.7.4.0/<OS>
    ```
    
    **Built with Repository File (Temporary Internet Access)**
    
    ```bash
    http://<web.server>/ambari/<OS>/Updates-Ambari-2.7.4.0
    ```
    
    where `<web.server> = FQDN` of the web server host, and `<OS>` is amazonlinux2, centos7, sles12, ubuntu16, ubuntu18, or debian9.

3. Place the `ambari.repo` file on the host you plan to use for the Ambari server:

    **For RHEL/CentOS/Oracle/Amazon Linux:**
    
    ```bash
    /etc/yum.repos.d/ambari.repo
    ```
    
    **For SLES:**
    
    ```bash
    /etc/zypp/repos.d/ambari.repo
    ```
    
    **For Debain/Ubuntu:**
    
    ```bash
    /etc/apt/sources.list.d/ambari.list
    ```

4. Edit the `/etc/yum/pluginconf.d/priorities.conf` file to add the following values:

    ```bash
    [main]
    enabled=1
    gpgcheck=0
    ```

### Next Steps

Proceed to [Installing Ambari]($InstallingAmbari) to install and setup Ambari Server.

### More Information

- [Setting Up a Local Repository with No Internet Access]($SettingUpALocalRepositoryWithTemporaryInternetAcce)
- [Setting up a Local Repository with Temporary Internet Access]($SettingUpALocalRepositoryWithNoInternetAccess)
