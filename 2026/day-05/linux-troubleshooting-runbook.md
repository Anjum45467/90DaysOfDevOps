# Linux Troubleshooting Runbook 

## Environment Basics
### 1.Uname -r 
```bash
Linux pu2vlinfrat56889.dsone.3ds.com 4.18.0-553.107.1.el8_10.x86_64 #1 SMP Tue Feb 17 05:52:05 EST 2026 x86_64 x86_64 x86_64 GNU/Linux
```
#### observation:
- System is running Red Hat Enterprise Linux 8 kernel.
- Architecture is x86_64.
- Kernel version is 4.18 which is stable for enterprise workloads.

---------

### 2.cat /etc/os-relese
```bash
NAME="Red Hat Enterprise Linux"
VERSION="8.10 (Ootpa)"
ID="rhel"
ID_LIKE="fedora"
VERSION_ID="8.10"
PLATFORM_ID="platform:el8"
PRETTY_NAME="Red Hat Enterprise Linux 8.10 (Ootpa)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:redhat:enterprise_linux:8::baseos"
HOME_URL="https://www.redhat.com/"
DOCUMENTATION_URL="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8"
BUG_REPORT_URL="https://bugzilla.redhat.com/"

REDHAT_BUGZILLA_PRODUCT="Red Hat Enterprise Linux 8"
REDHAT_BUGZILLA_PRODUCT_VERSION=8.10
REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux"
REDHAT_SUPPORT_PRODUCT_VERSION="8.10"
```
#### observation:
- Operating system identified as RHEL 8.10.
- Server belongs to Red Hat enterprise distribution.
- Useful for package management and troubleshooting compatibility issues.

----------

### 3.ls -lh dsplm
```bash
total 4.0K
drwxrwxr-x 11 anjum anjum  150 Apr  9 18:31 apps
drwxrwxr-x  3 anjum anjum   25 Mar 31 14:46 Extra
drwxrwxr-x 13 anjum anjum 4.0K Apr  1 12:19 logs
drwxrwxr-x  4 anjum anjum   28 Apr 21 17:52 media
drwxrwxr-x 13 anjum anjum  191 Apr  8 17:59 R2026x
```
#### observation:
- Filesystem is writable. /home directory is healthy. File permissions look correct (644). No space or permission errors.
