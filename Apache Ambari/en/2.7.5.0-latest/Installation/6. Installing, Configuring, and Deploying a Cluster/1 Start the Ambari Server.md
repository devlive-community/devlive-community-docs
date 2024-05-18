[TOC]

- Run the following command on the Ambari Server host:

    ```bash
    ambari-server start
    ```

- To check the Ambari Server processes:

    ```bash
    ambari-server status
    ```

- To stop the Ambari Server:

    ```bash
    ambari-server stop
    ```

    > If you plan to use an existing database instance for Hive or for Oozie, you must prepare to use an existing database **before** installing your Hadoop cluster.

On Ambari Server start, Ambari runs a database consistency check looking for issues. If any issues are found, Ambari Server **start will abort** and display the following message: `DB configs consistency check failed`. Ambari writes more details about database consistency check results to the `/var/log/ambari-server/ambari-server-check-database.log` file.

You can force Ambari Server to start by skipping this check with the following option:

```bash
ambari-server start --skip-database-check
```

If you have database issues, by choosing to skip this check, **do not make any changes to your cluster topology or perform a cluster upgrade until you correct the database consistency issues**. Please contact Hortonworks Support and provide the `ambari-server-check-database.log` output for assistance.

### Next Steps

[Install, Configure and Deploy a Hadoop cluster]($InstallingConfiguringAndDeployingACluster)

### More Information

- [Using a new or existing database with Hive](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Using-A-New-Or-Existing-Database-With-Hive)
- [Using an existing database with Oozie](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Using-An-Existing-Database-With-Oozie)
