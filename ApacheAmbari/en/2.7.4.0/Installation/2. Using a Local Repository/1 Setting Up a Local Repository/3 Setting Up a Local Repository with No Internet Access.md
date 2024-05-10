[TOC]

### Prerequisites

You must have completed the [Getting Started Setting up a Local Repository]($PreparingToSetUpALocalRepository) procedure.

- -

To finish setting up your local repository, complete the following:

### Steps

1. Obtain the compressed tape archive file (tarball) for the repository you want to create.
2. Copy the repository tarball to the web server directory and uncompress (untar) the archive:

    a. Browse to the web server directory you created.
    
    **For RHEL/CentOS/Oracle/Amazon Linux:**
    
    ```bash
    cd /var/www/html/
    ```
    
    **For SLES:**
    
    ```bash
    cd /srv/www/htdocs/rpms
    ```
    
    **For Debian/Ubuntu:**
    
    ```bash
    cd /var/www/html/
    ```
    
    b. Untar the repository tarballs and move the files to the following locations, where `<web.server>`, `<web.server.directory>`, `<OS>`, `<version>`, and `<latest.version>` represent the name, home directory, operating system type, version, and most recent release version, respectively:
    
    **Ambari Repository**

    Untar under `<web.server.directory>`.
    
    **HDF Stack Repositories**

    Create a directory and untar it under `<web.server.directory>/hdf`.
    
    **HDP Stack Repositories**
    
    Create a directory and untar it under `<web.server.directory>/hdp`.

3. Confirm that you can browse to the newly created local repositories, where `<web.server>`, `<web.server.directory>`, `<OS>`, `<version>`, and `<latest.version>` represent the name, home directory, operating system type, version, and most recent release version, respectively:

   **Ambari Base URL**
   
   `http://<web.server>/Ambari-2.7.4.0/<OS>`
   
   **HDF Base URL**
   
   `http://<web.server>/hdf/HDF/<OS>/3.x/updates/<latest.version>`
   
   **HDP Base URL**
   
   `http://<web.server>/hdp/HDP/<OS>/3.x/updates/<latest.version>`
   
   **HDP-UTILS Base URL**
   
   `http://<web.server>/hdp/HDP-UTILS-<version>/repos/<OS>`
   
   > Be sure to record these Base URLs. You will need them when installing Ambari and the cluster.

4. Optional: If you have multiple repositories configured in your environment, deploy the following plug-in on all the nodes in your cluster.

   a. **For RHEL/CentOS/Oracle 7:**
   
   ```bash
   yum install yum-plugin-priorities
   ```
   
   b. Edit the `/etc/yum/pluginconf.d/priorities.conf` file to add the following values:
   
   ```bash
   [main]
   enabled=1
   gpgcheck=0
   ```

### More Information

[Accessing Cloudera Repositories]($AccessingClouderaRepositories)
