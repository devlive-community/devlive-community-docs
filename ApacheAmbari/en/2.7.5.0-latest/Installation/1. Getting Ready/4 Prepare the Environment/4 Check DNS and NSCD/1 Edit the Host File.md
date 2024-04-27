[TOC]

1. Using a text editor, open the hosts file on every host in your cluster. For example:

    ```bash
    vi /etc/hosts
    ```

2. Add a line for each host in your cluster. The line should consist of the IP address and the FQDN. For example:
    
    ```bash
    1.2.3.4 <fully.qualified.domain.name>
    ```

    > Do `not` remove the following two lines from your hosts file. Removing or editing the following lines may cause various programs that require network functionality to fail.
    
    ```bash
    127.0.0.1 localhost.localdomain localhost
    ```
    
    ```bash
    ::1 localhost6.localdomain6 localhost6
    ```
