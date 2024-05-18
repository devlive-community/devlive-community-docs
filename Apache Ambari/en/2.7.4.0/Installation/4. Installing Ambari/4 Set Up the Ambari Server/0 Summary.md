[TOC]

Before starting the Ambari Server, you **must** set up the Ambari Server. Setup configures Ambari to talk to the Ambari database, installs the JDK and allows you to customize the user account the Ambari Server daemon will run as. The

```bash
ambari-server setup
```

command manages the setup process. Run the following command on the Ambari server host to start the setup process. You may also append Setup Options to the command.

```bash
ambari-server setup
```

Respond to the setup prompt:

1. If you have not temporarily disabled SELinux, you may get a warning. Accept the default (`y`), and continue.
2. By default, Ambari Server runs under `root`. Accept the default (`n`) at the `Customize user account for ambari-server daemon` prompt, to proceed as `root`. If you want to create a different user to run the Ambari Server, or to assign a previously created user, select `y` at the `Customize user account for ambari-server daemon` prompt, then provide a user name.
3. If you have not temporarily disabled `iptables` you may get a warning. Enter `y` to continue.
4. Select a JDK version to download. Enter 1 to download Oracle JDK 1.8.

    By default, Ambari Server setup downloads and installs Oracle JDK 1.8 and the accompanying Java Cryptography Extension (JCE) Policy Files.

5. To proceed with the default installation, accept the Oracle JDK license when prompted. You must accept this license to download the necessary JDK from Oracle. The JDK is installed during the deploy phase.

    Alternatively, you can enter 2 to download a Custom JDK. If you choose Custom JDK, you must manually install the JDK on all hosts and specify the Java Home path.
    
    > To install OpenJDK, use the Custom option. Be prepared to provide the valid JAVA_HOME value to Ambari. We strongly recommend that you install the JDK packages consistently on all hosts.

6. Review the GPL license agreement when prompted. To explicitly enable Ambari to download and install LZO data compression libraries, you must answer `y`. If you enter `n`, Ambari will not automatically install LZO on any new host in the cluster. In this case, you must ensure LZO is installed and configured appropriately. Without LZO being installed and configured, data compressed with LZO will not be readable. If you do not want Ambari to automatically download and install LZO, you must confirm your choice to proceed.
7. Select `n` at `Enter advanced database configuration` to use the default, embedded PostgreSQL database for Ambari. The default PostgreSQL database name is `ambari`. The default user name and password are `ambari/bigdata`. Otherwise, to use an existing PostgreSQL, MySQL/MariaDB or Oracle database with Ambari, select `y`.

   - If you are using an existing PostgreSQL, MySQL/MariaDB, or Oracle database instance, use one of the following prompts:

      > You must prepare an existing database instance, before running setup and entering advanced database configuration.
    
      > Using the **Microsoft SQL Server** or **SQL Anywhere** database options are not supported.

   - To use an existing Oracle instance, and select your own database name, user name, and password for that database, enter `2`.

       Select the database you want to use and provide any information requested at the prompts, including host name, port, Service Name or SID, user name, and password.

   - To use an existing MySQL/MariaDB database, and select your own database name, user name, and password for that database, enter `3`.

       Select the database you want to use and provide any information requested at the prompts, including host name, port, database name, user name, and password.

   - To use an existing PostgreSQL database, and select your own database name, user name, and password for that database, enter `4`.

       Select the database you want to use and provide any information requested at the prompts, including host name, port, database name, user name, and password.

8. At `Proceed with configuring remote database connection properties [y/n]` choose `y`.
9. Setup completes.

    > If your host accesses the Internet through a proxy server, you must configure Ambari Server to use this proxy server.

### More Information

- [Setup Options]($SetupOptions)
- [Configuring Ambari for Non-Root](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Configuring-Ambari-For-Non-Root)
- [Changing your JDK](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Changing-Your-JDK)
- [Configuring LZO compression](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Configuring-LZO-Compression)
- [Using an existing database with Ambari](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Using-An-Existing-Database-With-Ambari)
- [Setting up Ambari to use an Internet proxy server](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Setting-Up-Ambari-To-Use-An-Internet-Proxy-Server)
