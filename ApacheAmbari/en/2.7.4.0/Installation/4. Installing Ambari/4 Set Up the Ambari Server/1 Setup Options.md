[TOC]

The following options are frequently used for Ambari Server setup.

**-j (or --java-home)**

Specifies the JAVA_HOME path to use on the Ambari Server and all hosts in the cluster. By default when you do not specify this option, Ambari Server setup downloads the Oracle JDK 1.8 binary and accompanying Java Cryptography Extension (JCE) Policy Files to /var/lib/ambari-server/resources. Ambari Server then installs the JDK to /usr/jdk64.

Use this option when you plan to use a JDK other than the default Oracle JDK 1.8. If you are using an alternate JDK, you must manually install the JDK on all hosts and specify the Java Home path during Ambari Server setup. If you plan to use Kerberos, you must also install the JCE on all hosts.

This path must be valid on all hosts. For example:

```bash
ambari-server setup –j /usr/java/default
```

**--jdbc-driver**

Should be the path to the JDBC driver JAR file. Use this option to specify the location of the JDBC driver JAR and to make that JAR available to Ambari Server for distribution to cluster hosts during configuration. Use this option with the --jdbc-db option to specify the database type.

**--jdbc-db**

Specifies the database type. Valid values are: [postgres | mysql | oracle] Use this option with the --jdbc-driver option to specify the location of the JDBC driver JAR file.

**-s (or --silent)**

Setup runs silently. Accepts all the default prompt values, such as:

- User account "root" for the ambari-server
- Oracle 1.8 JDK (which is installed at /usr/jdk64). This can be overridden by adding the -j option and specifying an existing JDK path.
- Embedded PostgreSQL for Ambari DB (with database name "ambari")

    > By choosing the silent setup option and by not overriding the JDK selection, Oracle JDK will be installed and you will be agreeing to the Oracle Binary Code License agreement.
    
    > Do not use this option if you do not agree to the license terms.
    
    > If the Ambari Server is behind a firewall, you must instruct the ambari-server setup commad to use a proxy when downloading a JDK. To do so, define the http_proxy environment variable in the shell before running the setup command. For example:
    
    ```bash
    export http_proxy=http://{username}:{password}@{proxyHost}:{proxyPort}
    ambari-server setup
    ```
    
    > where {username} and {password} are optional.
    
    > If you do not define the http_proxy environment variable in a firewalled environment, the Oracle JDK download will not succeed.

If you want to run the Ambari Server as non-root, you must run setup in interactive mode. When prompted to customize the ambari-server user account, provide the account information.

**--enable-lzo-under-gpl-license**

Use this option to download and install LZO compression, subject to the General Public License.

**-v (or --verbose)**

Prints verbose info and warning messages to the console during Setup.

**-g (or --debug)**

Prints debug info to the console during Setup.

### More Information

- [JDK Requirements](https://supportmatrix.hortonworks.com/)
- [Configuring Ambari for Non-Root](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Configuring-Ambari-For-Non-Root)
- [Configuring LZO compression](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Configuring-LZO-Compression)
- [Oracle Java License Terms](http://www.oracle.com/technetwork/java/javase/terms/license/index.html)
