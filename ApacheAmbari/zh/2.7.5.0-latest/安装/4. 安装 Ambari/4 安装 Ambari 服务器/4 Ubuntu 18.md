[TOC]

在可以访问 Internet 的服务器主机上，使用命令行编辑器执行以下操作

### 步骤

1. 在安装 Ambari 之前，您必须更新 `ambari.list` 文件中的 `username` 和 `password` 。运行以下命令： **vi /etc/apt/sources.list.d/ambari.list**

    例如，输出显示以下内容：
    
   ```bash
   #VERSION_NUMBER=2.7.5.0-72
   #json.url = https://archive.cloudera.com/p/ambari/2.7.5.0-72//ubuntu18/HDP/hdpdev_urlinfo.json
   deb https://username:password@archive.cloudera.com/p/ambari/2.7.5.0-72/ubuntu16 Ambari main
   ```

2. 接下来，安装 Ambari。这还会安装默认的 PostgreSQL Ambari 数据库。

    ```bash
    apt-get install ambari-server
    ```

   > 当部署互联网访问权限有限或没有互联网访问权限的集群时，您应该使用替代方法提供对这些位的访问。

   > Ambari Server 默认使用嵌入式 PostgreSQL 数据库。安装 Ambari Server 时，PostgreSQL 软件包和依赖项必须可供安装。这些软件包通常作为操作系统存储库的一部分提供。请确认您有可用于 postgresql-server 软件包的适当存储库。

### 下一步

- [设置 Ambari 服务器]($SetUpTheAmbariServer)

### 更多信息

- [使用本地存储库]($UsingALocalRepository)

