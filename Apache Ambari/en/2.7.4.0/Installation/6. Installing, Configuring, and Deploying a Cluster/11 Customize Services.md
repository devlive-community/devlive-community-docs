[TOC]

The Customize Services step presents you with a set of tabs that let you review and modify your cluster setup. The Cluster Install wizard attempts to set reasonable defaults for each of the options. You are strongly encouraged to review these settings as your requirements might be more advanced.

![](https://cdn.north.devlive.org/images/2024/05/06/17149619321952.jpg)

Ambari will group the commonly customized configuration elements together into four categories: Credentials, Databases, Directories, and Accounts. All other configuration will be available in the All Configurations section of the Installation Wizard

### Credentials

Passwords for administrator and database accounts are grouped together for easy input. Depending on the services chosen, you will be prompted to input the required passwords for each item, and have the option to change the username used for administrator accounts

> Ranger and Atlas require strong passwords for your security. Hover over each property to see its password requirements. Passwords that do not meet these requirements will be highlighted on the All Configurations tab at the end of the **Customize Services** step.

### Databases

Some services require a backing database to function. For each service that has been chosen for install that requires a database, you will be asked to select which database should be used and configure the connectivity details for the selected database.

> By default, Ambari installs a new MySQL instance for the Hive Metastore and installs a Derby instance for Oozie. If you plan to use existing databases for MySQL/MariaDB, Oracle or PostgreSQL, modify the database type and host before proceeding. For a quick example on creating external databases on MariaDB, see Example: Install MariaDB for use with multiple components, in Administering Ambari.

> Using the **Microsoft SQL Server** or **SQL Anywhere** database options are not supported.

### Directories

Choosing the right directories for data and log storage is critical. Ambari chooses reasonable defaults based on the mount points available in your environment but you are strongly encouraged to review the default directory settings recommended by Ambari. In particular, confirm directories such as /tmp and /var are not being used for HDFS NameNode directories and DataNode directories under the HDFS tab.

### Accounts

The service account users and groups are also configurable from the Accounts tab. These are the operating system accounts the service components will run as. If these users do not exist on your hosts, Ambari will automatically create the users and groups locally on the hosts. If these users already exist, Ambari will use those accounts.

Depending on how your environment is configured, you might not allow groupmod or usermod operations. If this is the case, there are multiple options to choose how Ambari should handle user creation and modification:

**Use Ambari to Manage Service Accounts and Groups**

Ambari will create the service accounts and groups that are required for each service if they do not exist in /etc/password, and in /etc/group of the Ambari Managed hosts.

**Use Ambari to Manage Group Memberships**

Ambari will add or remove the service accounts from groups.

**Use Ambari to Manage Service Accounts UID's**

Ambari will be able to change the UID’s of all service accounts.

### All Configurations

Here you have an opportunity to review and revise the remaining configurations for your services. Browse through each configuration tab. Hovering your cursor over each of the properties, displays a brief description of what the property does. The number of service tabs shown here depends on the services you decided to install in your cluster. **Any service with configuration issues that require attention will show up in the bell icon with the number properties that need attention.**

![](https://cdn.north.devlive.org/images/2024/05/06/17149621733642.jpg)

The bell popover contains configurations that require your attention, configurations that are highly recommended to be reviewed and changed, and configurations that will be automatically changed based on Ambari’s recommendations unless you choose to opt out of those changes. Required Configuration must be addressed in order to proceed on to the next step in the Wizard. Carefully review the required and recommended settings and address issues before proceeding

After you complete Customizing Services, choose **Next**.

### Next Step

[Review]($Review)

### More Information

[Using an existing or installing a default database](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Using-An-Existing-Or-Installing-A-Default-Database)

[Understanding service users and groups](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Understanding-Service-Users-And-Groups)
