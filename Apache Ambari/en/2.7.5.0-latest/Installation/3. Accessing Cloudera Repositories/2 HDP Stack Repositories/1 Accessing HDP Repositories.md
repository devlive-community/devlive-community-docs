[TOC]

Starting with the **HDP 3.1.5** release, access to HDP repositories requires authentication. To access the binaries, you must first have the required authentication credentials (**username** and **password**).

Authentication credentials for new customers and partners are provided in an email sent from Cloudera to registered support contacts. Existing users can file a non-technical case within the support portal (https://my.cloudera.com) to obtain credentials.

Previously, HDP repositories were located on AWS S3. As of **HDP 3.1.5** / **Ambari 2.7.5**, repositories have been moved to https://archive.cloudera.com

When you obtain your authentication credentials, use them to form the URL where you can access the HDP repository in the HDP archive, as shown below. Insert your username and password at the front of the URL.

### Table 3.1. HDP Repository URLs

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
