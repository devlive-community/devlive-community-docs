[TOC]

Starting with the **Ambari 2.7.5** release, access to Ambari repositories requires authentication. To access the binaries, you must first have the required authentication credentials (**username** and **password**).

Authentication credentials for new customers and partners are provided in an email sent from Cloudera to registered support contacts. Existing users can file a non-technical case within the support portal (https://my.cloudera.com) to obtain credentials.

Previously, Ambari repositories were located on AWS S3. As of **HDP 3.1.5** / **Ambari 2.7.5**, repositories have been moved to https://archive.cloudera.com

When you obtain your authentication credentials, use them to form the URL where you can access the Ambari repository in the Ambari archive, as shown below. Insert your username and password at the front of the URL as shown.

For example, for Ambari 2.7.5 the complete Ambari repository URL looks like:

### Table 4.1. Ambari Repository URLs

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
