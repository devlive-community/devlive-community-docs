为了使 Ambari 在设置过程中与其部署和管理的主机进行通信，某些端口必须打开且可用。最简单的方法是暂时禁用 iptables，如下所示：

### RHEL/CentOS/Oracle/Amazon Linux

```bash
systemctl disable firewalld
service firewalld stop
```

### SLES

```bash
rcSuSEfirewall2 stop
chkconfig SuSEfirewall2_setup off
```

### Ubuntu

```bash
sudo ufw disable
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X
sudo iptables -t mangle -F
sudo iptables -t mangle -X
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```

### Debian

```bash
sudo iptables -X
sudo iptables -t nat -F
sudo iptables -t nat -X
sudo iptables -t mangle -F
sudo iptables -t mangle -X
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```

设置完成后可以重新启动 iptables。如果您环境中的安全协议阻止禁用 iptables，并且所有必需的端口均已打开且可用，则您可以继续启用 iptables。

Ambari 在 Ambari Server 设置过程中检查 iptables 是否正在运行。如果 iptables 正在运行，则会显示一条警告，提醒您检查所需端口是否已打开且可用。集群安装向导中的主机确认步骤还会对每个运行 iptables 的主机发出警告。
