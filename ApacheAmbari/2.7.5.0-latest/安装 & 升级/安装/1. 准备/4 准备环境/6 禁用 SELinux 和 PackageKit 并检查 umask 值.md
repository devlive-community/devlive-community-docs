1. 您必须禁用 SELinux 才能使 Ambari 安装程序正常运行。在集群中的每个主机上，输入：

```bash
setenforce 0
```

> 要永久禁用 SELinux，请在 `/etc/selinux/config` 中设置 SELINUX=disabled 这可确保 SELinux 在您重新启动计算机后不会自行打开。

2. 在运行 RHEL/CentOS 并安装了 PackageKit 的安装主机上，使用文本编辑器打开 `/etc/yum/pluginconf.d/refresh-packagekit.conf`。进行以下更改：

```bash
enabled=0
```

> 默认情况下，Debian、SLES 或 Ubuntu 系统上未启用 PackageKit。除非您专门启用了 PackageKit，否则对于 Debian、SLES 或 Ubuntu 安装主机，您可以跳过此步骤。

3. UMASK（用户掩码或用户文件创建掩码）设置在 Linux 计算机上创建新文件或文件夹时授予的默认权限或基本权限。大多数 Linux 发行版将 022 设置为默认 umask 值。 umask 值 022 授予新文件或文件夹的读、写、执行权限 755。 umask 值 027 授予新文件或文件夹的读、写、执行权限 750。

    Ambari、HDP 和 HDF 支持 umask 值 022（0022 功能等效）、027（0027 功能等效）。必须在所有主机上设置这些值。

    **UMASK 示例**

   设置当前登录会话的 umask：

    ```bash
    umask 0022
    ```
   
    检查当前 umask

    ```bash
    umask
    ```

   永久更改所有交互式用户的 umask：

    ```bash
    echo umask 0022 >> /etc/profile
    ```