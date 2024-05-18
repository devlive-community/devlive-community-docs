[TOC]

1. You must disable SELinux for the Ambari setup to function. On each host in your cluster, enter:
    
    ```bash
    setenforce 0
    ```
    
    > To permanently disable SELinux set SELINUX=disabled in /etc/selinux/config This ensures that SELinux does not turn itself on after you reboot the machine .

2. On an installation host running RHEL/CentOS with PackageKit installed, open `/etc/yum/pluginconf.d/refresh-packagekit.conf` using a text editor. Make the following change:

    ```bash
    enabled=0
    ```
    
    > PackageKit is not enabled by default on Debian, SLES, or Ubuntu systems. Unless you have specifically enabled PackageKit, you may skip this step for a Debian, SLES, or Ubuntu installation host.

3. UMASK (User Mask or User file creation MASK) sets the default permissions or base permissions granted when a new file or folder is created on a Linux machine. Most Linux distros set 022 as the default umask value. A umask value of 022 grants read, write, execute permissions of 755 for new files or folders. A umask value of 027 grants read, write, execute permissions of 750 for new files or folders.

    Ambari, HDP, and HDF support umask values of 022 (0022 is functionally equivalent), 027 (0027 is functionally equivalent). These values must be set on all hosts.
    
    **UMASK Examples:**

    Setting the umask for your current login session:
    
    ```bash
    umask 0022
    ```
    
    Checking your current umask:
    
    ```bash
    umask
    ```
    
    Permanently changing the umask for all interactive users:
    
    ```bash
    echo umask 0022 >> /etc/profile
    ```
