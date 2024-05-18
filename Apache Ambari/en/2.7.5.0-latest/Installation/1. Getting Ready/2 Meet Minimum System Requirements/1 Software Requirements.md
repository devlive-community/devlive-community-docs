[TOC]

On each of your hosts:

- `yum` and `rpm` (RHEL/CentOS/Oracle/Amazon Linux)
- `zypper` and `php_curl` (SLES)
- `apt` (Debian/Ubuntu)
- `scp`, `curl`, `unzip`, `tar`, `wget`, and `gcc*`
- OpenSSL (v1.01, build 16 or later)
- Python 2.7.12 (with python-devel*)

*Ambari Metrics Monitor uses a python library (psutil) which requires gcc and python-devel packages.
