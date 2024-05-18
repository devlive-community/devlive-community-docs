[TOC]

### About This Task

To have Ambari Server automatically install Ambari Agents on all your cluster hosts, you must set up password-less SSH connections between the Ambari Server host and all other hosts in the cluster. The Ambari Server host uses SSH public key authentication to remotely access and install the Ambari Agent.

> You can choose to manually install an Ambari Agent on each cluster host. In this case, you do not need to generate and distribute SSH keys.

### Steps

1. Generate public and private SSH keys on the Ambari Server host.

    ```bash
    ssh-keygen
    ```

2. Copy the SSH Public Key (id_rsa.pub) to the root account on your target hosts.

    ```bash
    .ssh/id_rsa
    .ssh/id_rsa.pub
    ```

3. Add the SSH Public Key to the authorized_keys file on your target hosts.

    ```bash
    cat id_rsa.pub >> authorized_keys
    ```

4. Depending on your version of SSH, you may need to set permissions on the .ssh directory (to 700) and the authorized_keys file in that directory (to 600) on the target hosts.

    ```bash
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys
    ```

5. From the Ambari Server, make sure you can connect to each host in the cluster using SSH, without having to enter a password.

    ```bash
    ssh root@<remote.target.host>
    ```

    where `<remote.target.host>` has the value of each host name in your cluster.

6. If the following warning message displays during your first connection: `Are you sure you want to continue connecting (yes/no)?` Enter `Yes`.

7. Retain a copy of the SSH Private Key on the machine from which you will run the web-based Ambari Install Wizard.

    > It is possible to use a non-root SSH account, if that account can execute sudo without entering a password.
