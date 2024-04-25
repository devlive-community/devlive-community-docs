### 关于此任务

要让 Ambari Server 自动在所有集群主机上安装 Ambari Agent，您必须在 Ambari Server 主机和集群中的所有其他主机之间设置无密码 SSH 连接。 Ambari Server 主机使用 SSH 公钥身份验证来远程访问和安装 Ambari Agent。

> 您可以选择在每个集群主机上手动安装 Ambari Agent。在这种情况下，您不需要生成和分发 SSH 密钥。

### 步骤

1. 在 Ambari Server 主机上生成公钥和私钥 SSH 密钥。

```bash
ssh-keygen
```

2. 将 SSH 公钥 (id_rsa.pub) 复制到目标主机上的 root 帐户。

```bash
.ssh/id_rsa
```

```bash
.ssh/id_rsa.pub
```

3. 将 SSH 公钥添加到目标主机上的authorized_keys 文件中。

```bash
cat id_rsa.pub >> authorized_keys
```

4. 根据您的 SSH 版本，您可能需要设置目标主机上 .ssh 目录（至 700）以及该目录中的 authorized_keys 文件（至 600）的权限。

```bash
chmod 700 ~/.ssh
```

```bash
chmod 600 ~/.ssh/authorized_keys
```

5. 从 Ambari Server 中，确保您可以使用 SSH 连接到集群中的每个主机，而无需输入密码。

```bash
ssh root@<remote.target.host>
```

其中 `<remote.target.host>` 具有集群中每个主机名的值。

6. 如果第一次连接时出现以下警告信息：`Are you sure you want to continue connecting (yes/no)?` 输入 `Yes`.

7. 在运行基于 Web 的 Ambari 安装向导的计算机上保留 SSH 私钥的副本。

   > 如果非 root SSH 帐户可以在不输入密码的情况下执行 sudo，则可以使用该帐户。
