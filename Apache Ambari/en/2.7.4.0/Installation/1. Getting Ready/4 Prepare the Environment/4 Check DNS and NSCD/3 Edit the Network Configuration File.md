[TOC]

1. Using a text editor, open the network configuration file on every host and set the desired network configuration for each host. For example:

    ```bash
    vi /etc/sysconfig/network
    ```

2. Modify the HOSTNAME property to set the fully qualified domain name.

    ```bash
    NETWORKING=yes
    ```
    
    ```bash
    HOSTNAME=<fully.qualified.domain.name>
    ```
