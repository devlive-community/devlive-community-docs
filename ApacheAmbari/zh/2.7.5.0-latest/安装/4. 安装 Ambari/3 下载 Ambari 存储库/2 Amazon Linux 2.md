[TOC]

在可以访问 Internet 的服务器主机上，使用命令行编辑器执行以下操作

### 步骤

1. 以 `root` 身份登录到您的主机。
2. 将 Ambari 存储库文件下载到安装主机上的目录。

    ```bash
    wget -nv https://username:password@archive.cloudera.com/p/ambari/amazonlinux2/2.x/updates/2.7.5.0/ambari.repo -O /etc/yum.repos.d/ambari.repo
    ```
    
    > 不要修改 `ambari.repo` 文件名。该文件预计在代理注册期间在 Ambari Server 主机上可用。

3. 通过检查存储库列表确认存储库已配置。

    ```bash
    yum repolist
    ```
    
    您应该在列表中看到类似于以下 Ambari 存储库的值。
    
    ```bash
    repo id                    repo name                                       status
    ambari-2.7.5.0-72          ambari Version - ambari-2.7.5.0-72            12
    epel/x86_64                Extra Packages for Enterprise Linux 7 - x86_64  11,387
    ol7_UEKR4/x86_64           Latest Unbreakable Enterprise Kernel Release 4
                                for Amazon Linux 2Server (x86_64)   295
    ol7_latest/x86_64          Amazon Linux 2Server Latest (x86_64)            18,642
    puppetlabs-deps/x86_64     Puppet Labs Dependencies El 7 - x86_64          17
    puppetlabs-products/x86_64 Puppet Labs Products El 7 - x86_64              225
     repolist: 30,578
    ```
    
    版本值因安装而异。
    
    > 当部署互联网访问受限或没有互联网访问的集群时，您应该使用替代方法提供对这些位的访问。

    > Ambari Server 默认使用嵌入式 PostgreSQL 数据库。安装 Ambari Server 时，PostgreSQL 软件包和依赖项必须可供安装。这些软件包通常作为操作系统存储库的一部分提供。请确认您有可用于 postgresql-server 软件包的适当存储库。

### 下一步

- [安装 Ambari 服务器]($InstallTheAmbariServer)
- [设置 Ambari 服务器]($SetUpTheAmbariServer)

### 更多信息

- [使用本地存储库]($UsingALocalRepository)
