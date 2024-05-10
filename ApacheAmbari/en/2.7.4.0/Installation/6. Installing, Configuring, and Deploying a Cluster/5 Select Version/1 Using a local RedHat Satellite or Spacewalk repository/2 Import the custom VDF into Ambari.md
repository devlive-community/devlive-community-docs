[TOC]

To import the custom VDF into Ambari, follow these steps:

1. In the cluster install wizard, **Select Version** step, click the drop down with the HDP version listed and select **Add Version**.

   ![](https://cdn.north.devlive.org/images/2024/05/10/17153411643292.jpg)

2. In **Add Version**, choose **Upload Version Definition File** and click **Choose File**. Browse to the directory on your local desktop where the VDF file has been stored, click **Choose File**, then click **Read Version Info**.

   ![](https://cdn.north.devlive.org/images/2024/05/10/17153416153315.jpg)

3. In **Select Version**, under **Repositories**, click **Use Local Repository**. signal to Ambari that repositories should not be downloaded from the internet.

   ![](https://cdn.north.devlive.org/images/2024/05/10/17153416198321.jpg)

   This signals to Ambari that repositories should not be downloaded from the internet.

4. In **Base URL**, type the protocol that prefixes your Base URL. For example: `https://`
5. Verify that the OS matches the operating system specific in the Base URL value.
6. Edit the **Name** of the repository to match the channel names in your RedHat Satellite or Spacewalk installation.

   ![](https://cdn.north.devlive.org/images/2024/05/10/17153416233035.jpg)

7. In **Repositories**, click the **Use RedHat Satellite/Spacewalk** checkbox.
8. Click **Next**.

### Next Step

[Install Options]($InstallOptions)

### More Information

[Setting up an Internet Proxy Server for Ambari](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Setting-Up-Ambari-To-Use-An-Internet-Proxy-Server)

[Using a Local Repository]($UsingALocalRepository)
