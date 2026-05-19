## Practice Notes (Linux Commands with Real Output)

---

### 1. ps -aux

```bash
ps -aux
```

**Output:**
```text
USER        PID   %CPU %MEM      VSZ     RSS    TTY   STAT START   TIME COMMAND
anjum     284466  0.0  0.0   268644   3996   pts/0   R+   16:52   0:00 ps -aux
```

**Explanation:**

- **USER** → Who started this process  
- **PID** → Process ID (unique)  
- **%CPU** → CPU usage  
- **%MEM** → RAM usage  
- **VSZ** → Total memory allocated  
- **RSS** → Actual RAM used  
- **TTY** → Terminal attached  
- **STAT** → Process state  

👉 This is very important — tells what the process is doing  

**Common Values:**
- S → Sleeping  
- R → Running  
- D → Waiting (I/O)  
- Z → Zombie ❌  
- Ss → Sleeping + session leader  
- I< → Idle kernel thread  

- **START** → When process started  
- **TIME** → CPU time used  
- **COMMAND** → What started the process  

---

### 2. TOP Command

```bash
top
```

**Output:**
```text
top - 17:46:41 up 3 days, 12:44, 1 user, load average: 0.01, 0.02, 0.05
Tasks: 272 total, 1 running, 271 sleeping, 0 stopped, 0 zombie
%Cpu(s): 0.7 us, 0.4 sy, 0.0 ni, 98.8 id
MiB Mem : 31887 total, 493 free, 16837 used, 14557 buff/cache
MiB Swap: 16136 total, 16136 free, 0 used
```

**Observations:**
- Server running since 3+ days → stable  
- Load average low → healthy system  
- No zombie processes → GOOD  

**CPU:**
- User CPU → 0.7%  
- System CPU → 0.4%  
- Idle → 98%  

**Memory:**
- Used → 16 GB  
- Cache → 14 GB (reusable)  
- Free → low (normal in Linux)  

👉 Linux uses memory cache to improve performance  

**Swap:**
- Not used → PERFECT  

---

### Process Table Example

```text
PID   USER     PR  NI   VIRT     RES    SHR S  %CPU %MEM   TIME+ COMMAND
981   jenkins  20   0   13.1g  472972  68448 S   0.3  1.4  7:40.47 java
```

| Column  | Meaning            |
|--------|--------------------|
| PID    | Process ID         |
| USER   | Owner              |
| PR     | Priority           |
| NI     | Nice value         |
| VIRT   | Virtual memory     |
| %CPU   | CPU usage          |
| %MEM   | RAM usage          |
| TIME+  | CPU time           |
| COMMAND| Application        |

---

### ☕ Find Java Processes

```bash
pgrep -fl java
```

---

### 🌳 Process Tree

```bash
pstree -p
```

---

### 🌐 Networking Commands

```bash
1.Check hostname resolution : getent hosts db.minutuscloud.com
2.Ping server (ICMP connectivity) : ping -c 4 10.0.7.75
3. Check if port is reachable (MOST IMPORTANT) : nc -zv 10.0.7.75 1433 oR nc -zv 10.0.7.75 3389
4. Alternative using telnet : telnet 10.0.7.75 3389
5. Trace route to server : traceroute 10.0.7.75
6.Continuous connectivity monitoring : watch -n 2 "nc -zv 10.0.7.75 1433"
ss -tulnp
ping -c 4 google.com
nslookup google.com
traceroute google.com
curl -I https://google.com
ip a
```

---

### ⚙️ Systemd Service Commands

#### Nginx Service
```bash
sudo apt install nginx -y
sudo systemctl start nginx
systemctl status nginx
```

**Output:**
```text
nginx.service - The nginx HTTP and reverse proxy server
Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled)
Active: active (running)
```

---

#### List All Services
```bash
systemctl list-units --type=service
```

---

#### SSH Service
```bash
systemctl status sshd
```

---

### 📜 Log Commands

```bash
journalctl
journalctl -u nginx -f
journalctl -u sshd
```

---

### Tail Logs

```bash
tail -n 50 <logfile>
```

---

### 🛠️ Service Inspection (crond)

```bash
systemctl status crond
```

---

### 🔁 Difference Between start and enable

- **start** → Starts service immediately  
- **enable** → Starts service on boot  
