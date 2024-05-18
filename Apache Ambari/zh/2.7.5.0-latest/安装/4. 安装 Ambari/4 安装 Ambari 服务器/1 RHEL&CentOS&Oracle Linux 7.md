[TOC]

在可以访问 Internet 的服务器主机上，使用命令行编辑器执行以下操作

### 步骤

1. 在安装 Ambari 之前，您必须更新 `ambari.repo` 文件中的 `username` 和 `password`。运行以下命令： **vi /etc/yum.repos.d/ambari.repo**

    例如，输出显示以下内容：
    
    ```bash
    #VERSION_NUMBER=2.7.5.0-72
    [ambari-2.7.5.0]
    #json.url = http://public-repo-1.hortonworks.com/HDP/hdp_urlinfo.json
    name=ambari Version - ambari-2.7.5.0
    baseurl=https://username:password@archive.cloudera.com/p/ambari/centos7/2.x/updates/2.7.5.0
    gpgcheck=1
    gpgkey=https://username:password@archive.cloudera.com/p/ambari/centos7/2.x/updates/2.7.5.0/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
    enabled=1
    priority=1
    ```

2. 接下来，安装 Ambari 位。这还会安装默认的 PostgreSQL Ambari 数据库。

    ```bash
    yum install ambari-server
    ```

3. 当提示确认事务和依赖性检查时输入 `y`。

    成功安装会显示类似于以下内容的输出：
    
    ```bash
    Installing : postgresql-libs-9.2.18-1.el7.x86_64         1/4
    Installing : postgresql-9.2.18-1.el7.x86_64              2/4
    Installing : postgresql-server-9.2.18-1.el7.x86_64       3/4
    Installing : ambari-server-2.7.5.0-124.x86_64           4/4
    Verifying  : ambari-server-2.7.5.0-124.x86_64           1/4
    Verifying  : postgresql-9.2.18-1.el7.x86_64              2/4
    Verifying  : postgresql-server-9.2.18-1.el7.x86_64       3/4
    Verifying  : postgresql-libs-9.2.18-1.el7.x86_64         4/4
    
    Installed:
      ambari-server.x86_64 0:2.7.5.0-72
    Dependency Installed:
     postgresql.x86_64 0:9.2.18-1.el7
     postgresql-libs.x86_64 0:9.2.18-1.el7
     postgresql-server.x86_64 0:9.2.18-1.el7
    Complete!
    ```
    
    > 接受有关信任 Hortonworks GPG 密钥的警告。该密钥将自动下载并用于验证 Hortonworks 的软件包。您将看到以下消息：
    
    ```bash
    Importing GPG key 0x07513CAD: Userid: "Jenkins (HDP Builds) <jenkin@hortonworks.com>" From : gpgkey=https://username:password@archive.cloudera.com/p/ambari/centos7/2.x/updates/2.7.5.0/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
    ```
   
    > 当部署互联网访问权限有限或没有互联网访问权限的集群时，您应该使用替代方法提供对这些位的访问。
    
    > Ambari Server 默认使用嵌入式 PostgreSQL 数据库。安装 Ambari Server 时，PostgreSQL 软件包和依赖项必须可供安装。这些软件包通常作为操作系统存储库的一部分提供。请确认您有可用于 postgresql-server 软件包的适当存储库。

### 下一步

- [设置 Ambari 服务器]($SetUpTheAmbariServer)

### 更多信息

- [使用本地存储库]($UsingALocalRepository)
