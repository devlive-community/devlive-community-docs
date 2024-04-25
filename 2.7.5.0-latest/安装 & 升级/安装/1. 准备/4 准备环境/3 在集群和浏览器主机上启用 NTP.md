集群中所有节点的时钟以及运行访问 Ambari Web 界面的浏览器的计算机必须能够相互同步。

要安装 NTP 服务并确保其在启动时启动，请在每台主机上运行以下命令：

### RHEL/CentOS/Oracle 7

```bash
yum install -y ntp
systemctl enable ntpd
```

### SLES

```bash
zypper install ntp
chkconfig ntp on
```

### Ubuntu

```bash
apt-get install ntp
update-rc.d ntp defaults
```

### Debian

```bash
apt-get install ntp
update-rc.d ntp defaults
```
