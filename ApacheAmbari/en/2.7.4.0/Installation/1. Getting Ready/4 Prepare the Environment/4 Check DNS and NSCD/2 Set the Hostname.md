[TOC]

1. Confirm that the hostname is set by running the following command:

    ```bash
    hostname -f
    ```
    
    This should return the `<fully.qualified.domain.name>` you just set.

2. Use the "hostname" command to set the hostname on each host in your cluster. For example:

    ```bash
    hostname <fully.qualified.domain.name>
    ```
