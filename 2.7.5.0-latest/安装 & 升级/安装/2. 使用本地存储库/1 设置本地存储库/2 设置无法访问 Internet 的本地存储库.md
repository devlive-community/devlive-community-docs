[TOC]

### 条件

您必须已完成 [开始设置本地存储库]($PreparingToSetUpALocalRepository) 过程。

- -

要完成本地存储库的设置，请完成以下操作：

### 步骤

1. 获取要创建的存储库的压缩磁带存档文件 (tarball)。
2. 将存储库 tarball 复制到 Web 服务器目录并解压缩 (untar) 存档：

   a. 浏览到您创建的 Web 服务器目录。

   #### RHEL/CentOS/Oracle/Amazon Linux:

    ```bash
    cd /var/www/html/
    ```

   #### SLES:

    ```bash
    cd /srv/www/htdocs/rpms
    ```

   #### Debian/Ubuntu:

    ```bash
    cd /var/www/html/
    ```

   b. 解压存储库 tarball 并将文件移动到以下位置，其中 `<web.server>`、`<web.server.directory>`、`<OS>`、`<version>` 和 `<latest.version>` 代表名称、主目录、操作系统类型、版本和最新发布版本分别为：

   #### Ambari Repository

   覆盖在 `<web.server.directory>` 下。

   #### HDF Stack Repositories

   创建一个目录并将其解压到 `<web.server.directory>/hdf` 下。

   #### HDP Stack Repositories

   创建一个目录并将其解压到 `<web.server.directory>/hdp` 下。

3. 确认您可以浏览到新创建的本地存储库，其中 `<web.server>`、`<web.server.directory>`、`<OS>`、`<version>` 和 `<latest.version>`  代表名称、主目录、操作系统类型、版本和最新发布版本分别为：

   #### Ambari URL
   `http://<web.server>/Ambari-2.7.5.0/<OS>`

   #### HDF URL
   `http://<web.server>/hdf/HDF/<OS>/3.x/updates/<latest.version>`

   #### HDP URL
   `http://<web.server>/hdp/HDP/<OS>/3.x/updates/<latest.version>`

   #### HDP-UTILS URL
   `http://<web.server>/hdp/HDP-UTILS-<version>/repos/<OS>`

   > 请务必记录这些基本 URL。安装 Ambari 和集群时将需要它们。

4. 可选：如果您的环境中配置了多个存储库，请在集群中的所有节点上部署以下插件。

   a. **RHEL/CentOS/Oracle 7:**

    ```bash
    yum install yum-plugin-priorities
    ```

   b. 编辑 `/etc/yum/pluginconf.d/priorities.conf` 文件以添加以下值：

    ```bash
    [main]
    enabled=1
    gpgcheck=0
    ```

### 更多信息

[获取公共存储库]($AccessingClouderaRepositories)
