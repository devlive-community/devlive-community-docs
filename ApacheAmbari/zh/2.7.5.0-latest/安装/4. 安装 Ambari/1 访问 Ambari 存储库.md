[TOC]

从 **Ambari 2.7.5** 版本开始，访问 Ambari 存储库需要身份验证。要访问二进制文件，您必须首先拥有所需的身份验证凭据（**用户名**和**密码**）。

Cloudera 发送给注册支持联系人的电子邮件中提供了新客户和合作伙伴的身份验证凭据。现有用户可以在支持门户 (https://my.cloudera.com) 中提交非技术案例以获得凭据。

此前，Ambari 存储库位于 AWS S3 上。从 **HDP 3.1.5** / **Ambari 2.7.5** 开始，存储库已移至 https://archive.cloudera.com

获取身份验证凭据后，使用它们形成可以访问 Ambari 存档中的 Ambari 存储库的 URL，如下所示。如图所示，在 URL 前面插入您的用户名和密码。

例如，对于 Ambari 2.7.5，完整的 Ambari 存储库 URL 如下所示：

### 表 4.1 Ambari 存储库 URL

<table summary="Ambari Repository URLs" border="1">
    <colgroup>
        <col width="33%" class="c1">
        <col width="33%" class="newCol2">
        <col width="34%" class="c2">
    </colgroup>
    <thead>
        <tr>
            <th>OS</th>
            <th>Format</th>
            <th>URL</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3">
                <p>RedHat 7</p>
                <p>CentOS 7</p>
                <p>Oracle Linux 7</p>
            </td>
            <td>Base URL</td>
            <td><code class="code">https://archive.cloudera.com/p/ambari/centos7/2.x/updates/2.7.5.0</code></td>
        </tr>
        <tr>
            <td>Repo URL</td>
            <td><code class="code">https://archive.cloudera.com/p/ambari/centos7/2.x/updates/2.7.5.0/ambari/repo</code></td>
        </tr>
        <tr>
            <td>Tarball md5 | asc</td>
            <td><code class="code">https://archive.cloudera.com/p/ambari/centos7/2.x/updates/2.7.5.0/ambari-2.7.5.0-centos7.tar.gz</code></td>
        </tr>
    </tbody>
</table>
