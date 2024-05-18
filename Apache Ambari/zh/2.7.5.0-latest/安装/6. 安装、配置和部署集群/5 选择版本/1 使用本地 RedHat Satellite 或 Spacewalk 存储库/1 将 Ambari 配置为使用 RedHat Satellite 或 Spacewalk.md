[TOC]

Ambari Server 使用版本定义文件 (VDF) 来了解版本中包含哪些产品和组件版本。为了使 Ambari 能够与 Satellite 或 Spacewalk 良好配合，您必须为集群中的特定操作系统版本创建自定义 VDF 文件，该文件告诉 Ambari 在安装或升级集群时要使用哪些 RedHat Satellite 或 Spacewalk 通道名称。

要创建自定义 VDF 文件，我们建议将现有 VDF 从我们的 [HDP 3.1.5 存储库]($HDP315Repositories) 表下载到本地桌面。下载后，在您的首选编辑器中打开 VDF 文件，并更改每个存储库的 <repoid/> 标签，以匹配之前配置的 Satellite 或 Spacewalk 通道名称。对于本示例，我在 Satellite 或 Spacewalk 中创建了以下频道：

### 表 6.1 Hortonworks 存储库的通道名称示例

<table summary="Example Channel Names for Hortonworks Repositories" border="1">
    <colgroup>
        <col width="50%" class="c1">
        <col width="50%" class="c2">
    </colgroup>
    <thead>
        <tr>
            <th><span class="bold"><strong>Hortonworks Repository</strong></span></th>
            <th><span class="bold"><strong>RedHat Satellite or Spacewalk Channel Name</strong></span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HDP-3.1.5.6091</td>
            <td>hdp_3.1.5.6091</td>
        </tr>
        <tr>
            <td>HDP-3.1-GPL*</td>
            <td>hdp_3.1_gpl</td>
        </tr>
        <tr>
            <td>HDP-UTILS-1.1.0.22</td>
            <td>hdp_utils_1.1.0.22</td>
        </tr>
    </tbody>
</table>

* 如果您的集群要使用 LZO 压缩，请参阅[配置 LZO 压缩](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Configuring-LZO-Compression)了解更多信息。
```xml
<repository-info>
    <os family="redhat7">
      <package-version>3_0_0_0_*</package-version>
      <repo>
 <baseurl>http://public-repo-1.hortonworks.com/HDP/centos7/3.x/updates/3.1.5.6091</baseurl>
        <repoid>hdp_3.1.5.6091</repoid>
        <reponame>HDP</reponame>
        <unique>true</unique>
      </repo>
      <repo>
 <baseurl>http://public-repo-1.hortonworks.com/HDP-GPL/centos7/3.x/updates/3.1.5.6091</baseurl>
        <repoid>hdp_3.1_gpl</repoid>
        <reponame>HDP-GPL</reponame>
        <unique>true</unique>
        <tags>
          <tag>GPL</tag>
        </tags>
      </repo>
      <repo>
 <baseurl>http://public-repo-1.hortonworks.com/HDP-UTILS-1.1.0.22/repos/centos7</baseurl>
        <repoid>hdp_utils_1.1.0.22</repoid>
        <reponame>HDP-UTILS</reponame>
        <unique>false</unique>
      </repo>
    </os>
  </repository-info>
```

### 下一步

[将自定义 VDF 导入 Ambari]($ImportTheCustomVDFIntoAmbari)
