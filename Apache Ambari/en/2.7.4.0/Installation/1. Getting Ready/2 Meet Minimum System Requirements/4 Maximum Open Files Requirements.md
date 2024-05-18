[TOC]

The recommended maximum number of open file descriptors is 10000, or more. To check the current value set for the maximum number of open file descriptors, execute the following shell commands on each host:

```bash
ulimit -Sn
```

```bash
ulimit -Hn
```

If the output is not greater than 10000, run the following command to set it to a suitable default:

```bash
ulimit -n 10000
```
