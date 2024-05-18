[TOC]

要将自定义 VDF 导入 Ambari，请执行以下步骤：

1. 在集群安装向导的 **Select Version** 步骤中，单击列出 HDP 版本的下拉列表，然后选择 **Add Version**。
2. 在 **Add Version** 中，选择 **Upload Version Definition File**，然后单击 **Choose File**。浏览到本地桌面上存储 VDF 文件的目录，单击 **Choose File**，然后单击 **Read Version Info**。

   ![](media/17148621919426/17148823476171.jpg)

3. 在 **Select Version** 中的 **Repositories** 下，单击 **Use Local Repository**。向 Ambari 发出信号，表明不应从互联网下载存储库。

   ![](media/17148621919426/17148823756012.jpg)

   这向 Ambari 发出信号，表明不应从互联网下载存储库。

4. 在 **Base URL** 中，键入基本 URL 前缀的协议。例如：`https://`
5. 验证操作系统是否与基本 URL 值中特定的操作系统匹配。
6. 编辑存储库的 **Name** 以匹配 RedHat Satellite 或 Spacewalk 安装中的通道名称。

   ![](media/17148621919426/17148824671291.jpg)

7. 在 **Repositories**, 点击 **Use RedHat Satellite/Spacewalk** 选择框.
8. 点击 **Next**.

### 下一步

[安装选项]($InstallOptions)

### 更多信息

[为 Ambari 设置 Internet 代理服务器](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Setting-Up-Ambari-To-Use-An-Internet-Proxy-Server)

[使用本地存储库]($UsingALocalRepository)
