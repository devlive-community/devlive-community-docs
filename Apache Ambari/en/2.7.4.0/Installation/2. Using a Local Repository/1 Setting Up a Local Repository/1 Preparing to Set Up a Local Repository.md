[TOC]

Before setting up your local repository, you must have met certain requirements.

- Selected an existing server, in or accessible to the cluster, that runs a supported operating system.
- Enabled network access from all hosts in your cluster to the mirror server.
- Ensured that the mirror server has a package manager installed such as yum (for RHEL, CentOS, Oracle, or Amazon Linux), zypper (for SLES), or apt-get (for Debian and Ubuntu).
- **Optional**: If your repository has temporary Internet access, and you are using RHEL, CentOS, Oracle, or Amazon Linux as your OS, installed yum utilities:

    ```bash
    yum install yum-utils createrepo
    ```
  
> After meeting these requirements, you can take steps to prepare to set up your local repository.

### Steps

1. Create an HTTP server:

    a. On the mirror server, install an HTTP server (such as Apache httpd) using the instructions provided on the Apache community website.

    b. Activate the server.

    c. Ensure that any firewall settings allow inbound HTTP access from your cluster nodes to your mirror server.

    > If you are using Amazon EC2, make sure that SELinux is disabled.

2. On your mirror server, create a directory for your web server.

    - For example, from a shell window, type:
   
        **For RHEL/CentOS/Oracle/Amazon Linux:**
   
        ```bash
        mkdir -p /var/www/html/
        ```

        **For SLES:**

        ```bash
        mkdir -p /srv/www/htdocs/rpms   
        ```

        **For Debian/Ubuntu:**

        ```bash
        mkdir -p /var/www/html/
        ```

    - If you are using a symlink, enable the `followsymlinks` on your web server.

### Next Steps

You next must set up your local repository, either with no Internet access or with temporary Internet access.

### More Information

[httpd.apache.org/download.cgi](http://httpd.apache.org/download.cgi)
