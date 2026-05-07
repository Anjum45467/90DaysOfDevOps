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

----------------
### 4.ps -o pid,pcpu,pmem,comm -p 1
```bash
PID %CPU %MEM COMMAND
      1  0.2  0.0 systemd
```
#### observation:
- PID 1 belongs to the `systemd` process which is the init process of the Linux system.
- CPU and memory utilization by systemd is minimal and within normal limits.
- No abnormal resource consumption observed from the core system service.

### 5.ps aux --sort=-%cpu | head -10

#### observation:
- Find the highest CPU consuming process 

### 6.ps aux --sort=-%mem | head -10

#### observation: 
- Find the highest RAM consuming process 

### 7.ps -p 929815 -o pid,ppid,%cpu,%mem,cmd

#### observation: 
-Inspect one process deeply PPID = parent process ID

### 8.free -h :
```bash 
total        used        free      shared  buff/cache   available
Mem:           31Gi        28Gi       376Mi       3.0Mi       1.9Gi       1.6Gi
Swap:          15Gi       5.1Gi        10Gi
```
#### Observation:
| Column       | Value  | What it means                                                              |
| ------------ | ------ | -------------------------------------------------------------------------- |
| `total`      | 31 GB  | Physical RAM installed on the machine                                      |
| `used`       | 28 GB  | RAM actively used by running processes/services                            |
| `free`       | 376 MB | RAM that is completely unused                                              |
| `shared`     | 3 MB   | Memory shared between processes (commonly tmpfs/shared memory)             |
| `buff/cache` | 1.9 GB | RAM used by Linux kernel for file cache and disk buffers                   |
| `available`  | 1.6 GB | Memory realistically available for new applications without heavy swapping |

-----------------------------
