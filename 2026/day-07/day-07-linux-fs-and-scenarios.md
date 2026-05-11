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
 
