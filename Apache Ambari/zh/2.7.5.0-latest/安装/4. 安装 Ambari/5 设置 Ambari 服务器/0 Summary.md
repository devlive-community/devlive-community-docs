[TOC]

在启动 Ambari 服务器之前，您**必须**设置 Ambari 服务器。安装程序将 Ambari 配置为与 Ambari 数据库通信、安装 JDK 并允许您自定义 Ambari 服务器守护程序将运行的用户帐户。这些设置可以通过命令行或在 Ambari 守护程序中设置。

```bash
ambari-server setup
```

命令管理设置过程。在 Ambari 服务器主机上运行以下命令以启动设置过程。您还可以将设置选项附加到命令中。

```bash
ambari-server setup
```

响应设置提示：

1. 如果您没有暂时禁用SELinux，您可能会收到警告。接受默认值 (`y`)，然后继续。
2. 默认情况下，Ambari Server 在 `root` 下运行。在 `Customize user account for ambari-server daemon` 提示符处接受默认值 ( `n` )，以 `root` 身份继续操作。如果要创建不同的用户来运行 Ambari 服务器，或分配以前创建的用户，请在 `Customize user account for ambari-server daemon` 提示符下选择 `y` ，然后提供用户名。
3. 如果您没有暂时禁用 `iptables` ，您可能会收到警告。输入 `y` 继续。
4. 选择要下载的JDK版本。输入 1 下载 Oracle JDK 1.8。

    默认情况下，Ambari Server 安装程序会下载并安装 Oracle JDK 1.8 以及随附的 Java 加密扩展 (JCE) 策略文件。

5. 要继续默认安装，请在出现提示时接受 Oracle JDK 许可证。您必须接受此许可证才能从 Oracle 下载必要的 JDK。 JDK 在部署阶段安装。

    或者，您可以输入 2 下载自定义 JDK。如果选择自定义 JDK，则必须在所有主机上手动安装 JDK 并指定 Java Home 路径。
    
    > 要安装 OpenJDK，请使用自定义选项。准备好向 Ambari 提供有效的 JAVA_HOME 值。我们强烈建议您在所有主机上一致地安装 JDK 软件包。

6. 出现提示时查看 GPL 许可协议。要显式启用 Ambari 下载并安装 LZO 数据压缩库，您必须回答 `y` 。如果输入 `n` ，Ambari 将不会自动在集群中的任何新主机上安装 LZO。在这种情况下，您必须确保 LZO 已正确安装和配置。如果没有安装和配置 LZO，则使用 LZO 压缩的数据将无法读取。如果您不希望 Ambari 自动下载并安装 LZO，则必须确认您的选择才能继续。
7. 在 `Enter advanced database configuration` 处选择 `n` ，以使用 Ambari 的默认嵌入式 PostgreSQL 数据库。默认 PostgreSQL 数据库名称是 `ambari` 。默认用户名和密码是 `ambari/bigdata` 。否则，要将现有 PostgreSQL、MySQL/MariaDB 或 Oracle 数据库与 Ambari 一起使用，请选择 `y` 。

   - 如果您使用现有的 PostgreSQL、MySQL/MariaDB 或 Oracle 数据库实例，请使用以下提示之一：

      > 在运行安装程序并输入高级数据库配置之前，您必须准备现有数据库实例。
    
      > 不支持使用 **Microsoft SQL Server** 或 **SQL Anywhere** 数据库选项。

   - 要使用现有 Oracle 实例，并为该数据库选择您自己的数据库名称、用户名和密码，请输入 `2` 。

       选择要使用的数据库，并根据提示提供所需的任何信息，包括主机名、端口、服务名称或 SID、用户名和密码。

   - 要使用现有的 MySQL/MariaDB 数据库，并为该数据库选择您自己的数据库名称、用户名和密码，请输入 `3` 。

       选择要使用的数据库，并根据提示提供所需的任何信息，包括主机名、端口、数据库名称、用户名和密码。

   - 要使用现有的 PostgreSQL 数据库，并为该数据库选择您自己的数据库名称、用户名和密码，请输入 `4` 。

       选择要使用的数据库，并根据提示提供所需的任何信息，包括主机名、端口、数据库名称、用户名和密码。

8. 在 `Proceed with configuring remote database connection properties [y/n]` 处，选择 `y` 。
9. 设置完成。

    > 如果您的主机通过代理服务器访问 Internet，则必须配置 Ambari Server 以使用该代理服务器。

### 更多信息

- [设置选项]($SetupOptions)
- [为非 Root 配置 Ambari](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Configuring-Ambari-For-Non-Root)
- [更改你的 JDK](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Changing-Your-JDK)
- [配置 LZO 压缩](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Configuring-LZO-Compression)
- [将现有数据库与 Ambari 结合使用](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Using-An-Existing-Database-With-Ambari)
- [设置 Ambari 以使用 Internet 代理服务器](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Setting-Up-Ambari-To-Use-An-Internet-Proxy-Server)
