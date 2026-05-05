Explanation:


USER → Who started this process


PID → Process ID (unique)


%CPU → CPU usage


%MEM → RAM usage


VSZ → Total memory allocated


RSS → Actual RAM used


TTY → Terminal attached


STAT → Process state


👉 This is very important — tells what the process is doing
Common Values:


S → Sleeping


R → Running


D → Waiting (I/O)


Z → Zombie ❌


Ss → Sleeping + session leader


I< → Idle kernel thread


Ss → systemd running normally


I< → kernel background tasks


START → When process started


TIME → CPU time used


COMMAND → What started the process



📊 2. TOP Command
top
Output:
top - 17:46:41 up 3 days, 12:44, 1 user, load average: 0.01, 0.02, 0.05Tasks: 272 total, 1 running, 271 sleeping, 0 stopped, 0 zombie%Cpu(s): 0.7 us, 0.4 sy, 0.0 ni, 98.8 idMiB Mem : 31887 total, 493 free, 16837 used, 14557 buff/cacheMiB Swap: 16136 total, 16136 free, 0 used
Observations:


Server running since 3+ days → stable


Load average low → healthy system


No zombie processes → GOOD


CPU:


User CPU → 0.3%


System CPU → 0.4%


Idle → 99%


Memory:


Used → 16 GB


Cache → 14 GB (reusable)


Free → low (normal in Linux)


👉 Linux uses memory cache to improve performance
Swap:


Not used → PERFECT



Process Table Example
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND981 jenkins 20 0 13.1g 472972 68448 S 0.3 1.4 7:40.47 java
ColumnMeaningPIDProcess IDUSEROwnerPRPriorityNINice valueVIRTVirtual memory%CPUCPU usage%MEMRAM usageTIME+CPU timeCOMMANDApplication

☕ Find Java Processes
pgrep -fl java
Output:


Multiple Java processes found


Indicates multiple Java-based services



🌳 Process Tree
pstree -p


Shows parent-child relationship



🌐 Networking Commands
Check Open Ports
ss -tulnp
Ping Test
ping -c 4 google.com
DNS Lookup
nslookup google.com
Trace Route
traceroute google.com
HTTP Check
curl -I https://google.com
IP Address
ip a

⚙️ Systemd Service Commands
1. Nginx Service
sudo apt install nginx -ysudo systemctl start nginxsystemctl status nginx
Output:
nginx.service - The nginx HTTP and reverse proxy serverLoaded: loaded (/usr/lib/systemd/system/nginx.service; disabled)Active: active (running)

2. List All Services
systemctl list-units --type=service
👉 Shows all running services

3. SSH Service
systemctl status sshd
👉 Used for remote login

📜 Log Commands
journalctl
journalctl -u nginx -fjournalctl -u sshd
👉 View system logs

Tail Logs
tail -n 50 <logfile>
👉 Shows last 50 lines

🛠️ Service Inspection (crond)
systemctl status crond
Observations:


Service is running


Running since long time → stable


Executes scheduled jobs



🔁 Difference Between start and enable


start → Starts service immediately


enable → Starts service on boot


---## 💯 Now:- Copy → paste into your file  - Save → commit → push  - It will look **perfect on GitHub** ✅  ---If you want next step 🚀  I can help you:- Fix your **README conflict**- Make your repo look like a **DevOps portfolio project**
