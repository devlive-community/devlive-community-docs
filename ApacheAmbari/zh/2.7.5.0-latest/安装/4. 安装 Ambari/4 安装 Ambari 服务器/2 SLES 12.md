[TOC]

在可以访问 Internet 的服务器主机上，使用命令行编辑器执行以下操作

### 步骤

1. 在安装 Ambari 之前，您必须更新 `ambari.repo` 文件中的 `username` 和 `password` 。运行以下命令： **vi /etc/zypp/repos.d/ambari.repo**

   例如，输出显示以下内容：
    
   ```bash
   [ambari-2.7.5.0]
   name=ambari Version - ambari-2.7.5.0
   enabled=1
   autorefresh=0
   username=<username>
   password=<password>
   baseurl=https://archive.cloudera.com/p/ambari/sles12/2.x/updates/2.7.5.0
   type=rpm-md
   priority=1
   gpgcheck=0
   gpgkey=https://archive.cloudera.com/p/ambari/sles12/2.x/updates/2.7.5.0/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
   ```

2. 接下来，安装 Ambari。这还会安装默认的 PostgreSQL Ambari 数据库。

    ```bash
    zypper install ambari-server
    ```

3. 当提示确认事务和依赖性检查时输入 `y`。

    成功安装会显示类似于以下内容的输出：
    
    ```bash
   Retrieving package postgresql-libs-8.3.5-1.12.x86_64 (1/4), 172.0 KiB (571.0 KiB unpacked)
   Retrieving: postgresql-libs-8.3.5-1.12.x86_64.rpm [done (47.3 KiB/s)]
   Installing: postgresql-libs-8.3.5-1.12 [done]
   Retrieving package postgresql-8.3.5-1.12.x86_64 (2/4), 1.0 MiB (4.2 MiB unpacked)
   Retrieving: postgresql-8.3.5-1.12.x86_64.rpm [done (148.8 KiB/s)]
   Installing: postgresql-8.3.5-1.12 [done]
   Retrieving package postgresql-server-8.3.5-1.12.x86_64 (3/4), 3.0 MiB (12.6 MiB unpacked)
   Retrieving: postgresql-server-8.3.5-1.12.x86_64.rpm [done (452.5 KiB/s)]
   Installing: postgresql-server-8.3.5-1.12 [done]
   Updating etc/sysconfig/postgresql...
   Retrieving package ambari-server-2.7.4.0-118.noarch (4/4), 99.0 MiB (126.3 MiB unpacked)
   Retrieving: ambari-server-2.7.4.0-118.noarch.rpm [done (3.0 MiB/s)]
   Installing: ambari-server-2.7.4.0-118 [done]
    ambari-server 0:off 1:off 2:off 3:on 4:off 5:on 6:off
    ```

    > 当部署互联网访问权限有限或没有互联网访问权限的集群时，您应该使用替代方法提供对这些位的访问。
    
    > Ambari Server 默认使用嵌入式 PostgreSQL 数据库。安装 Ambari Server 时，PostgreSQL 软件包和依赖项必须可供安装。这些软件包通常作为操作系统存储库的一部分提供。请确认您有可用于 postgresql-server 软件包的适当存储库。

### 下一步

- [设置 Ambari 服务器]($SetUpTheAmbariServer)

### 更多信息

- [使用本地存储库]($UsingALocalRepository)
