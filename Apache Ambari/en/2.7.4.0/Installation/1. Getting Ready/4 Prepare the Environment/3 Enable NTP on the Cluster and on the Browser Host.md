[TOC]

The clocks of all the nodes in your cluster and the machine that runs the browser through which you access the Ambari Web interface must be able to synchronize with each other.

To install the NTP service and ensure it's ensure it's started on boot, run the following commands on each host:

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
