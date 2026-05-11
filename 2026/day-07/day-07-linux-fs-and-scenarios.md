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
###### 1)How do you check if the 'nginx' service is running?
####### My Solution (Step by step):

Step 1: Check service status
```bash
systemctl status nginx
```
- Ans)systemctl status nginx 
