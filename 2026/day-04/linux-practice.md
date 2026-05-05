##practice note using real commands and real-world expected output##

1.ps -aux :
o/p :
USER        PID   %CPU %MEM      VSZ     RSS    TTY         STAT    START      TIME      COMMAND
anjum     284466   0.0   0.0    268644   3996   pts/0        R+     16:52      0:00        ps -aux

User : who started this process
PID  : process ID - Unique number for each process - Unique number for each process
CPU  : How much CPU this process is using
MEM  : How much RAM it is using
VSZ  : Total memory allocated (including unused)
RSS  : Real Memory - Actual RAM being used
TTY  : Terminal attached
STAT : Process State

This is VERY important — tells what process is doing

Common values:

S → Sleeping (waiting)
R → Running
D → Waiting (I/O)
Z → Zombie (bad 😬)
Ss → Sleeping + session leader
I< → Idle kernel thread

Ss → systemd is running normally
I< → kernel background tasks

START : When process started
TIME : Total CPU time used - process has used CPU for 28 mins total
COMMAND : what actaully had started the process

2.TOP :
top - 17:46:41 up 3 days, 12:44,  1 user,  load average: 0.01, 0.02, 0.05
Tasks: 272 total,   1 running, 271 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.7 us,  0.4 sy,  0.0 ni, 98.8 id,  0.0 wa,  0.2 hi,  0.0 si,  0.0 st
MiB Mem :  31887.6 total,    493.0 free,  16837.6 used,  14557.1 buff/cache
MiB Swap:  16136.0 total,  16136.0 free,      0.0 used.  14298.6 avail Mem


top : current time
server running since 3+ days (good stable)
1 user logged in
load average: 0.02, 0.02, 0.05
Load average = system pressure

Tasks (process summary):
Total processes = 272
Only 2 actively running
Most are sleeping (normal)
❌ No zombie → GOOD (no issue)


%Cpu(s):  0.3 us,  0.4 sy,  0.0 ni, 99.0 id
us → user CPU → 0.3%
sy → system CPU → 0.4%
id → idle → 99% 🔥

MiB Mem :  31887 total, 492 free, 16838 used, 14557 buff/cache
Used = 16 GB
Cache = 14 GB (can be reused)
Free = low → NORMAL in Linux

👉 Linux uses memory for cache to improve performancee

MiB Swap: 16136 total, 16136 free
Swap is NOT used at all → PERFECT

PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
981 jenkins   20   0   13.1g 472972  68448 S   0.3   1.4   7:40.47 java

| Column  | Meaning          |
| ------- | ---------------- |
| PID     | Process ID       |
| USER    | Who owns process |
| PR      | Priorities       |
| NI      | Nice Value       |
| VIRT    | Total virtual memory allocated
|  %CPU   | CPU usage        |
| %MEM    | RAM usage        |
| TIME+   | Total CPU time   |
| COMMAND | What app         |


### 2. Find Java processes
Command:
pgrep -fl java

Output (brief):
- Multiple Java processes found (963, 981, 1063, 1083, 2812)
- Indicates multiple Java-based services running


3. pstree -p
- Observed parent-child relationship of processes

# Networking Commands

1. ss -tulnp
- Observed open ports and services (e.g., SSH on port 22)

2. ping -c 4 google.com
- Verified network connectivity with successful responses

3. nslookup google.com
- Resolved domain name to IP address

4. traceroute google.com
- Observed network path and hops

5. curl -I https://google.com
- Checked HTTP response (status 200 OK)

6. ip a
- Displayed system IP address and network interfaces



#Include 2 service commands (systemctl status, systemctl list-units, etc.)
1.sudo apt install nginx -y
sudo systemctl start nginx
systemctl status nginx
o/p :
nginx.service - The nginx HTTP and reverse proxy server
Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
Active: active (running) since Tue 2026-04-28 12:59:25 IST; 4s ago
Process: 686342 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
Process: 686340 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS
Process: 686338 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS


2.systemctl list-units --type=service  (List All Services)
o/p : This command shows ALL running services in system

3.SECOND SERVICE (SSH) remote login service
systemctl status  sshd


##log commands
1.journalctl (journalctl is a command used to view logs collected by systemd (the system manager in Linux).
It reads logs from systemd journal
journalctl -u nginx -f
journalctl -u sshd

2.tail -n 50 <logfile>
Shows last 50 lines of log file

###Pick one service on your system (example: ssh, cron, docker) and inspect it
1.systemctl status crond
Active: running (since Apr 28)
Loaded: enabled = ❌ (disabled at boot)
Main PID: 771101
Multiple worker processes are running
Service is running manually but not enabled on boot
Note : The difference between enable ans start is
start → starts the service right now
enable → makes the service start automatically on boot
