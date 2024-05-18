[TOC]

In order to build up the cluster, the Cluster Install wizard prompts you for general information about how you want to set it up. You need to supply the FQDN of each of your hosts. The wizard also needs to access the private key file you created when you set up password-less SSH. Using the host names and key file information, the wizard can locate, access, and interact securely with all hosts in the cluster.

### Steps

1. In **Target Hosts**, enter your list of host names, one per line.

    You can use ranges inside brackets to indicate larger sets of hosts. For example, for host01.domain through host10.domain use `host[01-10].domain`
    
    > If you are deploying on EC2, use the `internal Private DNS` host names.

2. If you want to let Ambari automatically install the Ambari Agent on all your hosts using SSH, select **Provide your SSH Private Key** and either use the **Choose File** button in the **Host Registration Information** section to find the private key file that matches the public key you installed earlier on all your hosts or cut and paste the key into the text box manually.

3. Enter the user name for the SSH key you have selected. If you do not want to use `root`, you must provide the user name for an account that can execute `sudo` without entering a password. If SSH on the hosts in your environment is configured for a port other than 22, you can change that also.

4. If you do not want Ambari to automatically install the Ambari Agents, select **Perform manual registration**.
5. Choose **Register and Confirm** to continue.

### Next Step

[Confirm Hosts]($ConfirmHosts)

### More Information

[Set Up Password-less SSH]($SetUpPasswordLessSSH)

[Installing Ambari Agents Manually](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.4.0/Administering-Ambari/Installing-Ambari-Agents-Manually)
