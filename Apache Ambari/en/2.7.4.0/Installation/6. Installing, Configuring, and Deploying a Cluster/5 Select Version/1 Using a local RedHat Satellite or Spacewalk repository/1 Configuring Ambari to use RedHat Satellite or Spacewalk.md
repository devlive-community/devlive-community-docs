[TOC]

The Ambari Server uses Version Definition Files (VDF) to understand which product and component versions are included in a release. In order for Ambari to work well with Satellite or Spacewalk, you must create a custom VDF file for the specific Operating System versions in your cluster that tells Ambari which RedHat Satellite or Spacewalk channel names to use when installing or upgrading the cluster.

To create a custom VDF file, we recommend downloading an existing VDF from the our [HDP 3.1.4 Repositories]($HDP314Repositories) table to your local desktop. Once downloaded, open the VDF file in your preferred editor and change the `<repoid/>` tags for each repository to match the Satellite or Spacewalk channel names previously configured. For this example, I’ve created the following channels in Satellite or Spacewalk:

### Table 6.1. Example Channel Names for Hortonworks Repositories

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
            <td>HDP-3.1.4.0</td>
            <td>hdp_3.1.4.0</td>
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

* If LZO compression is going to be used in your cluster, see [Configuring LZO Compression](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Configuring-LZO-Compression) for more information.

```xml
<repository-info>
    <os family="redhat7">
        <package-version>3_0_0_0_*</package-version>
        <repo>
            <baseurl>https://archive.cloudera.com/p/HDP/3.x/3.1.4.0/centos7/</baseurl>
            <repoid>hdp_3.1.4.0</repoid>
            <reponame>HDP</reponame>
            <unique>true</unique>
        </repo>
        <repo>
            <baseurl>https://archive.cloudera.com/p/HDP-GPL/3.x/3.1.4.0/centos7/</baseurl>
            <repoid>hdp_3.1_gpl</repoid>
            <reponame>HDP-GPL</reponame>
            <unique>true</unique>
            <tags>
                <tag>GPL</tag>
            </tags>
        </repo>
        <repo>
            <baseurl>https://archive.cloudera.com/p/HDP-UTILS/1.1.0.22/repos/centos7/</baseurl>
            <repoid>hdp_utils_1.1.0.22</repoid>
            <reponame>HDP-UTILS</reponame>
            <unique>false</unique>
        </repo>
    </os>
</repository-info>
```

### Next Step

[Import the custom VDF into Ambari]($ImportTheCustomVDFIntoAmbari)
