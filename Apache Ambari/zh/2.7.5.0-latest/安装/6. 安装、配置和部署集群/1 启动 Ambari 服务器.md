[TOC]

- 在 Ambari Server 主机上运行以下命令：

    ```bash
    ambari-server start
    ```

- 要检查 Ambari Server 进程：

    ```bash
    ambari-server status
    ```

- 停止 Ambari 服务器：

    ```bash
    ambari-server stop
    ```

    > 如果您计划将现有数据库实例用于 Hive 或 Oozie，则必须在安装 Hadoop 集群 **之前** 准备使用现有数据库。

在 Ambari Server 启动时，Ambari 运行数据库一致性检查以查找问题。如果发现任何问题，Ambari Server **启动将中止**并显示以下消息： `DB configs consistency check failed` 。 Ambari 将有关数据库一致性检查结果的更多详细信息写入 `/var/log/ambari-server/ambari-server-check-database.log` 文件。

您可以使用以下选项跳过此检查来强制 Ambari Server 启动：

```bash
ambari-server start --skip-database-check
```

如果您遇到数据库问题，请选择跳过此检查，**不要对集群拓扑进行任何更改或执行集群升级，直到纠正数据库一致性问题**。请联系 Hortonworks 支持并提供 `ambari-server-check-database.log` 输出以获取帮助。

### 下一步

[安装、配置和部署集群]($InstallingConfiguringAndDeployingACluster)

### 更多信息

- [将新的或现有的数据库与 Hive 结合使用](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Using-A-New-Or-Existing-Database-With-Hive)
- [将现有数据库与 Oozie 结合使用](https://docs.devlive.org/read/apache-ambari-en-administering-2.7.5.0/Using-An-Existing-Database-With-Oozie)
