# Linux File System Hierarchy & Scenario-Based

###  Part 1: Linux File System Hierarchy
-  `/` (root) - The starting point of everything
- `/home` - User home directories.hidden files include .bashrc , .profile , .ssh , .config
- `/root` - Root user's home directory
- `/etc` - Configuration files eg: /etc/hosts , /etc/passwd → list of all users on the system (not passwords, those are in /etc/shadow),
           /etc/apt → package manager config , /etc/cron.d → scheduled tasks (cron jobs)
- `/var/log` - This is where every service writes its logs

	     - dpkg.log (576KB) — every package installed/removed, with timestamps.You can see ca-certificates-java was installed on Apr
	     
	     - bootstrap.log — system startup log
             
	     - btmp / wtmp — login/logout history, failed login attempts 
             
	     - /var/log/nginx/access.log     → every web request
             
	     - /var/log/nginx/error.log      → nginx errors
             
	     - /var/log/syslog               → general system events
             
	     - /var/log/auth.log             → SSH logins, sudo usage
             
	     - /var/log/docker/              → container logs
- `/tmp` - Temporary files
         - This directory is for files that don't need to survive a reboot. Linux automatically cleans it on restart.
	 - What you just saw:
         - node-compile-cache, phantomjs, .lock files — apps storing temp data while running
	 - We created /tmp/anjum_test.txt and it worked instantly — no permissions needed!

	 - Special thing about /tmp permissions — drwxrwxrwt:

	 - The t at the end is called the sticky bit
	 - It means: everyone can write files here, but you can only delete your own files
	 - So one user can't delete another user's temp files
- `proc, sys` — virtual directories, they don't exist on disk, Linux creates them in memory
- `/bin and /usr/bin`  — /bin is just a symlink (shortcut) pointing to /usr/bin. So on modern Ubuntu, they are literally identical. When                         you type ls, Linux looks in /bin which redirects to /usr/bin/ls.
- `/opt`  —   stands for optional. It's where software goes when it is not installed through the system's package manager (apt/yum).

          
          - apt install git    →  goes to /usr/bin/git     (system managed)
          - Manual install     →  goes to /opt/git/        (you manage it)


#### output of each directory : 
- ls -l /home  — 
```bash
- claude — home folder for user claude
- ubuntu — home folder for user ubuntu
- "I would use this when setting up a new user on a server or accessing another user's files and SSH keys."
```
-ls -la /root  —
```bash
- bashrc — root user's terminal settings and aliases
- ssh — root's SSH keys for connecting to servers
- "I would use this when doing system-level administration tasks that require root access."
```
- /var/log  —
```bash
- dpkg.log (576KB) — full history of packages installed/removed
- bootstrap.log (60KB) — system startup log
- "I would use this when an app crashes or a deployment fails and I need to find the error by checking logs."
```
- ls -lh /tmp  — 
```bash
- anjum_test.txt — the file we created earlier, still there!
- node-compile-cache — temp cache created by Node.js
- "I would use this when I need to download and test a script quickly without cluttering my home directory, knowing it will auto-clean on reboot."
```
- ls -l /bin        # shows: /bin -> usr/bin (symlink!)
- ls -l /usr/bin    # shows 1067 commands like ls, git, curl, python3
```bash  
/bin is a symlink → usr/bin
/usr/bin has actual binaries like git, curl, python3
"I would use this when I need to find where a command is installed using which, or when writing scripts where I need the full path of a binary."
```
- ls -l /opt  —
```bash
- google/chrome — Google Chrome installed manually
- pw-browsers/chromium-1194 — Chromium installed by Playwright testing tool
- " would use this when manually installing tools like Jenkins, Terraform, or vendor software that isn't available through apt."
```
--------------------------------------------
### Part 2: Scenario-Based Practice
 
#### Understanding How to Approach Scenarios :
##### Check if a service is running:

1)How do you check if the 'nginx' service is running?

My Solution (Step by step):

Step 1: Check service status
```bash
systemctl status nginx
```
Why this command? It shows if the service is active, failed, or stopped.

Step 2: If service is not found, list all services
```bash
systemctl list-units --type=service
```
Why this command? To see what services exist on the system

Step 3: Check if service is enabled on boot
```bash
systemctl is-enabled nginx
```
Why this command? To know if it will start automatically after reboot

What I learned: Always check status first, then investigate based on what you see.

### practice:
Scenario 1: Service Not Starting
```bash
A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.
```
When a service fails, i will investigate in this order:

- Status → Logs → Config → Fix
- commands: 
- 1.systemctl status myapp : Is it active, failed, or inactive .
```bash
Output to look for:
Active: failed (Result: exit-code)   ← something crashed
Loaded: ...myapp.service; disabled   ← not enabled on boot
```
- 2 — Read the logs : journalctl -u myapp -n 50
```bash
What it tells :
The actual error message — why did it fail?
In our example: Cannot find module '/opt/myapp/server.js' → file is missing!
```
-  3 — Check if enabled on boot : systemctl is-enabled myapp
```bash
What it tells :
enabled → will auto-start on reboot 
disabled → will NOT start on reboot 
```
- 4 — Confirm it's not running : ss -tlnp | grep 3000
```bash
What it tells you:
Is the app actually listening on its port?
No output = app is definitely not running
ss = socket status (modern replacement for netstat)
```
2)Scenario 2: High CPU Usage
```bash
Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?
```
My Solution (Step by step):

- 1 — top → Live view of all processes
```bash
top -bn1 | head -20
```bash
| Field              | What it means                                 |
| ------------------ | --------------------------------------------- |
| `%Cpu(s): 94.3 us` | 94% CPU in use — server is struggling         |
| `id: 1.5`          | only 1.5% idle — nearly zero breathing room   |
| `%CPU column`      | sort by this — highest number is your culprit |
| `COMMAND column`   | tells you exactly which app is eating CPU     |
```
-  2 — ps aux → Snapshot sorted by CPU
```bash 
ps aux --sort=-%cpu | head -10
Why use this over top?
- top is live/interactive — hard to copy output
- ps aux gives a clean snapshot — easy to share with your team or paste in tickets
| Flag           | Meaning                       |
| -------------- | ----------------------------- |
| `a`            | show processes from all users |
| `u`            | show user/owner column        |
| `x`            | include background processes  |
| `--sort=-%cpu` | sort by CPU, highest first    |
| `head -10`     | show only top 10              |
```
- 3 — uptime → Is this a new problem or ongoing?
```bash
uptime
o/p: 
load average: 3.85, 3.90, 3.78
               ↑      ↑     ↑
	       1min   5min  15min

- The golden rule:
Load average should be LESS than your CPU count

1 CPU  → load average above 1.0 = problem
4 CPUs → load average above 4.0 = problem

All three numbers high → problem has been going on for 15+ minutes
Only 1min high → just started, maybe a spike
```
- 4 — lsof -p <PID> → What is that process actually doing?
```bash
lsof -p 9821
Once you find the bad PID from top or ps, use lsof to see:

- Which files it has open
- How many network connections it has
- What ports it's using

In our example: 890 open connections on port 3000 — app is getting hammered with traffic, causing high CPU.
```
```bash
FIX:
systemctl restart myapp    → restart service
kill -9 <PID>              → force kill if frozen
journalctl -u myapp -n 100 → check why it happened
```
scenario 3: Finding Service Logs
```bash
A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?
```
My Solution (Step by step):

- 1 — Check status first : systemctl status docker
```bash
| What you see               | What it means                                  |
| -------------------------- | ---------------------------------------------- |
| `Active: active (running)` | service is fine, check logs for app errors     |
| `Active: failed`           | service crashed — logs will show why           |
| `Loaded: disabled`         | not enabled on boot — won’t survive reboot     |
| `Last 5 log lines`         | quick preview — often enough to spot the issue |
```
- 2 — Read last N lines of logs : journalctl -u docker -n 50
```bash
| Flag         | Meaning                                        |
| ------------ | ---------------------------------------------- |
| `-u docker`  | only show logs for docker service              |
| `-n 50`      | last 50 lines — change to 100 or 200 if needed |
| `--no-pager` | print directly, don't open scroll view         |
| `-b`         | only logs since last boot                      |
```
- 3 — Follow logs in real time : journalctl -u docker -f
```bash
Use this when: Developer says "the error happens when I do X" — you run this, they trigger the action, you watch the error appear live. Press Ctrl+C to stop.

Exactly like tail -f /var/log/something.log but for systemd services.
```
- 4 — Show ONLY errors : journalctl -u docker -p err -n 20
```bash 
Use this when logs are massive and you just want errors fast.
Priority levels from worst to best:
0 = emerg    → system is unusable
1 = alert    → action must be taken NOW
2 = crit     → critical condition
3 = err      → error condition   ← -p err shows this and above
4 = warning  → warning
5 = notice   → normal but significant
6 = info     → informational
7 = debug    → debug messages
```
```bash
SCENARIO: Finding Service Logs

COMMANDS IN ORDER:
1. systemctl status docker          → quick health check + last 5 lines
2. journalctl -u docker -n 50       → read last 50 log lines
3. journalctl -u docker -f          → follow live (Ctrl+C to stop)
4. journalctl -u docker -p err -n 20 → show only errors

USEFUL EXTRAS:
journalctl -u docker --since "1 hour ago"   → time filter
journalctl -u docker -b                     → since last boot
journalctl --disk-usage                     → how much space logs use

KEY RULE:
systemd services → logs live in journald → use journalctl
file-based apps  → logs live in /var/log → use tail/cat/grep
```
Scenario 4: File Permissions Issue
```bash
A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?
```
My Solution (Step by step):

-  1 — Check current permissions : ls -l /home/user/backup.sh
```bash
-rw-r--r-- 1 root root 63 May 11 backup.sh
How to read -rw-r--r--:
- rw- r-- r--
│  │   │   │
│  │   │   └── Others : r-- = read only
│  │   └─────── Group  : r-- = read only
│  └─────────── Owner  : rw- = read + write
└────────────── file type: - = regular file, d = directory
No x anywhere = nobody can execute it = Permission denied
```
- 2 — Fix it with chmod : chmod +x /home/user/backup.sh
```bash
| Style    | Command          | Meaning                    |
| -------- | ---------------- | -------------------------- |
| Symbolic | `chmod +x file`  | add execute for everyone   |
| Symbolic | `chmod u+x file` | add execute for owner only |
| Numeric  | `chmod 755 file` | `rwxr-xr-x`                |
| Numeric  | `chmod 644 file` | `rw-r--r--`                |
```
- 3 — Verify it worked : ls -l /home/user/backup.sh
```bash
-rwxr-xr-x 1 root root 63 May 11 backup.sh
Now you can see x in all three groups — owner, group, others can all execute it 
```
- Run it!
- ./backup.sh
- Backing up files...
- Backup complete!
