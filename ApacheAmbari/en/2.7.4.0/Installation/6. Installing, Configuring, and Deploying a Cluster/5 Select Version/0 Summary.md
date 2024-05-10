[TOC]

In this Step, you will select the software version and method of delivery for your cluster. Using a Private Repository requires Internet connectivity. Using a Local Repository requires you have configured the software in a repository available in your network.

### Choosing Stack

The available versions are shown in TABs. When you select a TAB, Ambari attempts to discover what specific version of that Stack is available. That list is shown in a DROPDOWN. For that specific version, the available Services are displayed, with their Versions shown in the TABLE.

![](https://cdn.north.devlive.org/images/2024/05/10/17153410743803.jpg)

### Choosing Version

If Ambari has access to the Internet, the specific Versions will be listed as options in the DROPDOWN. If you have a Version Definition File for a version that is not listed, you can click **Add Version…** and upload the VDF file. In addition, a **Default Version Definition** is also included in the list if you do not have Internet access or are not sure which specific version to install.

> In case your Ambari Server has access to the Internet but has to go through an Internet Proxy Server, be sure to setup the Ambari Server for an Internet Proxy.

![](https://cdn.north.devlive.org/images/2024/05/10/17153411643292.jpg)

### Choosing Repositories

Ambari gives you a choice to install the software from the Private Repositories (if you have Internet access) or Local Repositories. Regardless of your choice, you can edit the Base URL of the repositories. The available operating systems are displayed and you can add/remove operating systems from the list to fit your environment.

The UI displays repository Base URLs based on Operating System Family (OS Family). Be sure to set the correct OS Family based on the Operating System you are running.

#### redhat7

Red Hat 7, CentOS 7, Oracle Linux 7, Amazon Linux 2

#### sles12

SUSE Linux Enterprise Server 12

#### ubuntu14

Ubuntu 14

#### ubuntu16

Ubuntu 16

#### ubuntu18

Ubuntu 18

#### debian9

Debian 9

### Advanced Options

There are advanced repository options available.

- **Skip Repository Base URL validation (Advanced):** When you click **Next**, Ambari will attempt to connect to the repository Base URLs and validate that you have entered a validate repository. If not, an error will be shown that you must correct before proceeding.
- **Use RedHat Satellite/Spacewalk:** This option will only be enabled when you plan to use a Local Repository. When you choose this option for the software repositories, you are responsible for configuring the repository channel in Satellite/Spacewalk and confirming the repositories for the selected **stack version** are available on the hosts in the cluster.

### More Information

[Using a local RedHat Satellite or Spacewalk repository]($UsingALocalRedHatSatelliteOrSpacewalkRepository)
