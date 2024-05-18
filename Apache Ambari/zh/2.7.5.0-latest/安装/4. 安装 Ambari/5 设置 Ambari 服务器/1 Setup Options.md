[TOC]

以下选项经常用于 Ambari Server 设置。

**-j (or --java-home)**

指定要在 Ambari Server 和集群中的所有主机上使用的 JAVA_HOME 路径。默认情况下，如果您不指定此选项，Ambari Server 安装程序会将 Oracle JDK 1.8 二进制文件和随附的 Java 加密扩展 (JCE) 策略文件下载到 /var/lib/ambari-server/resources。然后，Ambari Server 将 JDK 安装到 /usr/jdk64。

当您计划使用默认 Oracle JDK 1.8 以外的 JDK 时，请使用此选项。如果您使用备用 JDK，则必须在所有主机上手动安装 JDK，并在 Ambari Server 设置期间指定 Java Home 路径。如果您计划使用 Kerberos，则还必须在所有主机上安装 JCE。

该路径必须在所有主机上都有效。例如：

```bash
ambari-server setup –j /usr/java/default
```

**--jdbc-driver**

应该是 JDBC 驱动程序 JAR 文件的路径。使用此选项指定 JDBC 驱动程序 JAR 的位置，并使该 JAR 可用于 Ambari Server，以便在配置期间分发到集群主机。将此选项与 --jdbc-db 选项结合使用来指定数据库类型。

**--jdbc-db**

指定数据库类型。有效值为：[postgres | mysql | mysql | oracle] 将此选项与 --jdbc-driver 选项结合使用来指定 JDBC 驱动程序 JAR 文件的位置。

**-s (or --silent)**

安装程序静默运行。接受所有默认提示值，例如：

- ambari 服务器的用户帐户 `root`
- Oracle 1.8 JDK（安装在/usr/jdk64）。这可以通过添加 -j 选项并指定现有的 JDK 路径来覆盖。
- Ambari DB 的嵌入式 PostgreSQL（数据库名称为 `ambari`）

    > 通过选择静默安装选项并且不覆盖 JDK 选择，将安装 Oracle JDK，并且您将同意 Oracle 二进制代码许可协议。
    
    > 如果您不同意许可条款，请勿使用此选项。
    
    > 如果 Ambari 服务器位于防火墙后面，则必须指示 ambari-server setup 命令在下载 JDK 时使用代理。为此，请在运行 setup 命令之前在 shell 中定义 http_proxy 环境变量。例如：

    ```bash
    export http_proxy=http://{username}:{password}@{proxyHost}:{proxyPort}
    ambari-server setup
    ```
    
    > 其中 {username} 和 {password} 是可选的。
    
    > 如果在防火墙环境中未定义 http_proxy 环境变量，Oracle JDK 下载将不会成功。

如果要以非 root 身份运行 Ambari Server，则必须以交互模式运行安装程序。当提示自定义 ambari-server 用户帐户时，请提供帐户信息。

**--enable-lzo-under-gpl-license**

使用此选项下载并安装 LZO 压缩，并遵守通用公共许可证。

**-v (or --verbose)**

在安装过程中将详细信息和警告消息打印到控制台。

**-g (or --debug)**

在安装过程中将调试信息打印到控制台。

### 更多信息

- [JDK 要求](https://supportmatrix.hortonworks.com/)
- [为非 Root 配置 Ambari](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Configuring-Ambari-For-Non-Root)
- [配置 LZO 压缩](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Configuring-LZO-Compression)
- [Oracle Java 许可条款](http://www.oracle.com/technetwork/java/javase/terms/license/index.html)
