[TOC]

从 **HDP 3.1.5** 版本开始，访问 HDP 存储库需要身份验证。要访问二进制文件，您必须首先拥有所需的身份验证凭据（**用户名**和**密码**）。

Cloudera 发送给注册支持联系人的电子邮件中提供了新客户和合作伙伴的身份验证凭据。现有用户可以在支持门户 (https://my.cloudera.com) 中提交非技术案例以获得凭据。

此前，HDP 存储库位于 AWS S3 上。从 **HDP 3.1.5** / **Ambari 2.7.5** 开始，存储库已移至 https://archive.cloudera.com

获取身份验证凭据后，使用它们形成可以访问 HDP 存档中的 HDP 存储库的 URL，如下所示。在 URL 前面插入您的用户名和密码。

### HDP 存储库 URL

<table summary="HDP Repository URLs" border="1">
    <colgroup>
        <col width="20%" class="c1">
        <col width="20%" class="c2">
        <col width="20%" class="newCol3">
        <col width="20%" class="newCol5">
        <col width="20%" class="newCol4">
    </colgroup>
    <thead>
        <tr>
            <th>OS</th>
            <th>Version Number</th>
            <th>Repository Name</th>
            <th>Format</th>
            <th>URL</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3">Red Hat 7</td>
            <td>HDP-3.1.5.6091</td>
            <td>HDP</td>
            <td>Base URL</td>
            <td>https://archive.cloudera.com/p/HDP/centos7/3.x/updates/3.1.5.6091/</td>
        </tr>
        <tr>
            <td>HDP-3.1.5.6091</td>
            <td>HDP</td>
            <td>Repo URL</td>
            <td>https://archive.cloudera.com/p/HDP/centos7/3.x/updates/3.1.5.6091/hdp.repo</td>
        </tr>
        <tr>
            <td>HDP-3.1.5.6091</td>
            <td>HDP</td>
            <td>Tarball md5 | asc</td>
            <td>https://archive.cloudera.com/p/HDP/centos7/3.x/updates/3.1.5.6091/HDP-3.1.5.6091-centos7-rpm.tar.gz</td>
        </tr>
    </tbody>
</table>
