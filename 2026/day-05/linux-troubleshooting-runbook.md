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
### 7. ps aux --sort=-%cpu | head -3
```bash
USER       PID %CPU %MEM COMMAND
webapp  929815  4.0 30.3 java
```
#### observation:
- Java web application consuming highest CPU resources.
- Memory usage is high but expected for enterprise Java applications.

-------------------

### 8.df -h 
```bash
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs         16G     0   16G   0% /dev
tmpfs            16G  888K   16G   1% /dev/shm
tmpfs            16G  1.2M   16G   1% /run
tmpfs            16G     0   16G   0% /sys/fs/cgroup
/dev/sda4       482G  181G  301G  38% /
/dev/sda2       2.0G  427M  1.6G  21% /boot
/dev/sda1       511M  5.9M  506M   2% /boot/efi
tmpfs           3.2G   16K  3.2G   1% /run/user/42
tmpfs           3.2G  8.0K  3.2G   1% /run/user/47937
```
#### observation:
| Filesystem  | Size | Used | Available | Use% | Mounted On        | Meaning                                                                                |
| ----------- | ---- | ---- | --------- | ---- | ----------------- | -------------------------------------------------------------------------------------- |
| `devtmpfs`  | 16G  | 0    | 16G       | 0%   | `/dev`            | Virtual filesystem managed by Linux kernel for device files like disks, USB, terminals |
| `tmpfs`     | 16G  | 888K | 16G       | 1%   | `/dev/shm`        | Temporary RAM-based shared memory filesystem                                           |
| `tmpfs`     | 16G  | 1.2M | 16G       | 1%   | `/run`            | Stores runtime process data in memory                                                  |
| `tmpfs`     | 16G  | 0    | 16G       | 0%   | `/sys/fs/cgroup`  | Used for Linux control groups (resource management for processes/containers)           |
| `/dev/sda4` | 482G | 181G | 301G      | 38%  | `/`               | Main root filesystem where OS, apps, logs, and user data exist                         |
| `/dev/sda2` | 2.0G | 427M | 1.6G      | 21%  | `/boot`           | Stores Linux kernel and bootloader files                                               |
| `/dev/sda1` | 511M | 5.9M | 506M      | 2%   | `/boot/efi`       | EFI partition used by UEFI firmware during boot                                        |
| `tmpfs`     | 3.2G | 16K  | 3.2G      | 1%   | `/run/user/42`    | Runtime temp storage for user session (UID 42)                                         |
| `tmpfs`     | 3.2G | 8.0K | 3.2G      | 1%   | `/run/user/47937` | Runtime temp storage for logged-in user session                                        |
-------------------
### 9.du -sh /var/log
```bash
2.1G    /var/log
```
#### observation: 
- Log directory size checked successfully

-----------
### 10.ss -tulpn
```bash
Netid  State    Recv-Q  Send-Q  Local Address:Port  Peer Address:Port  Process
tcp    LISTEN   0       128     0.0.0.0:22           0.0.0.0:*          sshd
tcp    LISTEN   0       511     0.0.0.0:80           0.0.0.0:*          nginx
tcp    LISTEN   0       511     0.0.0.0:443          0.0.0.0:*          nginx
udp    UNCONN   0       0       0.0.0.0:68           0.0.0.0:*          dhclient
```
### observation:
- ss -tulpn is asking your computer: "Which doors are open and who is standing behind them?"
- state
 - LISTEN   = door is open, someone is waiting inside
 - UNCONN   = door is open but nobody's really waiting (UDP thing)
 - ESTAB    = a visitor is ALREADY inside talking
