[TOC]

### 步骤

1. 从公共存储库下载 `ambari.repo` 文件：

    ```bash
    https://username:password@archive.cloudera.com/p/ambari/<OS>/2.x/updates/2.7.5.0/ambari.repo
    ```
   
    `<OS>` – centos7, sles12, ubuntu16, ubuntu 18, or debian9

2. 编辑 `ambari.repo` 文件并替换设置本地存储库时获取的 Ambari 基本 URL `baseurl`。

    ```bash
    [Updates-Ambari-2.7.5.0]
    name=Ambari-2.7.5.0-Updates
    baseurl=INSERT-BASE-URL
    gpgcheck=1
    gpgkey=https://username:password@archive.cloudera.com/p/ambari/centos7/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins
    enabled=1
    priority=1
    ```

    > 您可以通过设置 gpgcheck =0 来禁用 GPG 检查。或者，您可以保持启用检查，但将 gpgkey 替换为本地存储库中 GPG-KEY 的 URL。

    #### 本地存储库的基本 URL

    ##### 使用存储库 tarball 构建（无 Internet 访问）

    ```bash
    http://<web.server>/Ambari-2.7.5.0/<OS>
    ```
    
    ##### 使用存储库文件构建（临时互联网访问）
    
    ```bash
    http://<web.server>/ambari/<OS>/Updates-Ambari-2.7.5.0
    ```
    
    其中 `<web.server>` = Web 服务器主机的 FQDN，`<OS>` 是 amazonlinux2、centos7、sles12、ubuntu16、ubuntu18 或 debian9。

3. 将 `ambari.repo` 文件放置在您计划用于 Ambari 服务器的主机上：

    #### RHEL/CentOS/Oracle/Amazon Linux:

    ```bash
    /etc/yum.repos.d/ambari.repo
    ```
   
    #### SLES:

    ```bash
    /etc/zypp/repos.d/ambari.repo
    ```
   
    #### Debain/Ubuntu:

    ```bash
    /etc/apt/sources.list.d/ambari.list
    ```

4. 编辑 `/etc/yum/pluginconf.d/priorities.conf` 文件以添加以下值：

    ```bash
    [main]
    enabled=1
    gpgcheck=0
    ```

### 下一步

继续 [安装 Ambari]($InstallingAmbari) 以安装和设置 Ambari Server。

### 更多信息

- [设置无法访问 Internet 的本地存储库]($SettingUpALocalRepositoryWithNoInternetAccess)
- [设置具有临时 Internet 访问权限的本地存储库]($SettingUpALocalRepositoryWithTemporaryInternetAcce)
