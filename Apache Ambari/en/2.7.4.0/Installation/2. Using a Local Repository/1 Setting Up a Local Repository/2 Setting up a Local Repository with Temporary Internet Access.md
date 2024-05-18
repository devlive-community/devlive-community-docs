[TOC]

### Prerequisites

You must have completed the [Getting Started Setting up a Local Repository]($PreparingToSetUpALocalRepository) procedure.

- -

To finish setting up your local repository, complete the following:

### Steps

1. Install the repository configuration files for Ambari and the Stack on the host.
2. Confirm repository availability;

    **For RHEL, CentOS, Oracle or Amazon Linux:**

    ```bash
    yum repolist
    ```

    **For SLES:**

    ```bash
    zypper repos
    ```

    **For Debian and Ubuntu:**

    ```bash
    dpkg-list
    ```

3. Synchronize the repository contents to your mirror server:

   - Browse to the web server directory:

        **For RHEL, CentOS, Oracle or Amazon Linux:**
    
        ```bash
        cd /var/www/html/
        ```
    
        **For SLES:**
    
        ```bash
        cd /srv/www/htdocs/rpms
        ```
    
        **For Debian and Ubuntu:**
    
        ```bash
        cd /var/www/html/
        ```

   - For Ambari, create the `ambari` directory and reposync:

       ```bash
       mkdir -p ambari/<OS>
       ```
  
       ```bash
       cd ambari/<OS>
       ```
  
       ```bash
       reposync -r Updates-Ambari-2.7.4.0
       ```

      In this syntax, the value of `<OS>` is amazonlinux2, centos7, sles12, ubuntu16, ubuntu18, or debian9.
    
      > Due to a known issue in version 1.1.31-2 of the Debian 9 reposync, we advise using reposync version 11.3.1-3 or above when working on a Debian 9 host.

   - For Hortonworks Data Platform (HDP) stack repositories, create the `hdp` directory and reposync:

       ```bash
       mkdir -p hdp/<OS>
       ```
  
       ```bash
       cd hdp/<OS>
       ```
  
       ```bash
       reposync -r HDP-<latest.version>
       ```
  
       ```bash
       reposync -r HDP-UTILS-<version>
       ```

   - For HDF Stack Repositories, create an `hdf` directory and reposync.

       ```bash
       mkdir -p hdf/<OS>
       ```
  
       ```bash
       cd hdf/<OS>
       ```
  
       ```bash
       reposync -r HDF-<latest.version>
       ```

4. Generate the repository metadata:

    **For Ambari:**
    
    ```bash
    createrepo <web.server.directory>/ambari/<OS>/Updates-Ambari-2.7.4.0
    ```
    
    **For HDP Stack Repositories:**
    
    ```bash
    createrepo <web.server.directory>/hdp/<OS>/HDP-<latest.version>
    ```

    ```bash
    createrepo <web.server.directory>/hdp/<OS>/HDP-UTILS-<version>
    ```
    
    **For HDF Stack Repositories:**
    
    ```bash
    createrepo <web.server.directory>/hdf/<OS>/HDF-<latest.version>
    ```

5. Confirm that you can browse to the newly created repository:

    **Ambari Base URL**
    
    ```bash
    http://<web.server>/ambari/<OS>/Updates-Ambari-2.7.4.0
    ```
    
    **HDF Base URL**
    
    ```bash
    http://<web.server>/hdf/<OS>/HDF-<latest.version>
    ```
    
    **HDP Base URL**
    
    ```bash
    http://<web.server>/hdp/<OS>/HDP-<latest.version>
    ```
    
    **HDP-UTILS Base URL**
    
    ```bash
    http://<web.server>/hdp/<OS>/HDP-UTILS-<version>
    ```

    Where:

     - `<web.server>` – The FQDN of the web server host
     - `<version>` – The Hortonworks stack version number
     - `<OS>` – centos7, sles12, ubuntu16, ubuntu 18, or debian9

    > Be sure to record these Base URLs. You will need them when installing Ambari and the Cluster.

6. Optional. If you have multiple repositories configured in your environment, deploy the following plug-in on all the nodes in your cluster.

    a. Install the plug-in.

    **For RHEL/CentOS/Oracle 7:**

    ```bash
    yum install yum-plugin-priorities
    ```

    b. Edit the `/etc/yum/pluginconf.d/priorities.conf` file to add the following:

    ```bash
    [main]
    enabled=1
    gpgcheck=0
    ```

### More Information

[Accessing Cloudera Repositories]($AccessingClouderaRepositories)
