
####Commands to be remember######
##Navigateion and Files 
1. ls ---- listing the files 
2. ls -l ----long listing 
3. ls -a ------ listing all hidden files as well 
4. ls -t ------- list the files with the last time modefied 
5. cd ---- change directory 
6. cd .. ---- will take you one directory back 
7. cmp A B ----- it will compare A and B files no out put if both are identical if different then yess 
8. diff A B -------- it will going to compare A and B and give output for what is different 
9. pwd = present working directory 
10. mkdir anjum = it will create anjum directory 
11. mv A B = it will rename also it will move one from one source to destination
12. cp A B = it will going to copy from one source to the destination
13. cp -r X Y -------it will recursivly copy from X to Y with all its content 
14. rm X --- it will remove X permanently 
15. rm -rf x ---- remove with recursively and with the force
16. touch ---- creates the files 
17. cat ---- view content of the file
18. cat -b x ---- it will going to view and display the line numbers as well 

-----

##View and Edit 
19. wc x --- will display word count of x 
20. head x ---- displays starting 10 lines 
21. head -n x ---- displays the starting lines with numbers 
22. tail x ---- displays the ending lines 
23. tail -n 5 file -----it will display end of the 5 lines of the file 
24. tail -n +1 file ----- it will display the lines from start with numbering 
25. tail -f file ------ live monitoring of a file i
26. less file-name ----- 


----


##Search and find 
1. .Grep patt src = search for pattern in source
2. grep -r patt src = Recursive search in directory 
3. grep -v patt X = Lines Not matching pattern 
4. grep -l patt X Files containing pattern 
5. grep -i patt X = case insensitive search 
6. find = find files in the system 
7. find /src -name '*.sh' = find files all who are ending with *.sh 
8. find /home -size +1M = find files larger than 1 MB 
9. locate name = find files/directory by name 
10. sort X = Sort files alphabeticaly/numerically 

----

##File Transfer 
1. ssh user@host -- conect to host as user 
2. ssh -p port user@host --- Connect using specific port 
3. scp -p port --- SCP using specific port 
4. sftp user@host --- secure file transfer session 
5. sftp -p port user@host ---- SFTP using specific port 
6. rsync -a p1 p2 --- sync preserving attributes 
7. rsync -avz host:p1 ---- sync remote --> local with compress 

----

## disk usage 
1. df --- Display free disk space 
2. du -- show files and folders sizes on disk 
3. du -ah --- human readable disk usage 
4. du -sh --- Total usage f current directory 
5. du -h ---- free used on mounted filesystem 
6. du -i ---- free used inodes 
7. fdisk -l --- list partition size and types 
8. free -h --- memory in human readable units 
9. free -m : memory in MB 
10. free -g : memory in GB 

-----

##User Management 
1. who : will display whi is logged in 
2. w : users online and what they are doing 
3. users : list current users 
4. whoami : display your current user 
5. id : display user id and group id 
6. last : last user who logged in 
7. groupadd gp1: create group name gp1 
8. useradd -m ab1 : create account ab1 with home dir
9. userdel ab1 : delete account  ab1
10. usermod -aG gp1 ab1 : add user to group gp1 


----

## Hardware 
1. dmesg : kernal ring buffer message 
2. cat /proc/cpuinfo : CPU information 
3. cat /proc/meminfo : Meomery information 
4. lspci -tv : PCI device tree (verbose)
5. lsusb -tv : UDB device tree (verbose)
6. dmidecode : Hardware and BIOS version info 
7. hdparm -i /dev/sda : Disk sda information 
8. hdparm -tT /dev/sda : Read speed test on sda 
9. badloacks -s /dev/sda : Test for unreadable blocks 

----

## Process Management 
1. cmd & : Run command in background 
2. ps : show process status 
3. pa -A / ps -a : All running process 
4. ps -ef : Detail process overview 
5. top : shows live process info 
6.  htop : shows interactive process viewer
7. kill PID : kill process by PID 
8. killall proc1 : kill all processed name proc1 
9. lsof : list all open files 
10. lsof -u root : files open by root user 
11. mpstat 1 : CPU stats  updated every second 
12. vmstat 1 : virtaul memory stats per second 
13. iostat 1 : I/O stats per second 
14. tcpdump -i eth0 : capture packets on eth0 
15. watch df -h : periodic updates of df -h 

---

## i/o redirection  
1. echo TEXT : Display text or variable 
2. echo -n TEXT : omit trailing newline 
3. cmd > file : Redirect output (overwrite)
4. cmd >$ file : Redierct output , suppress display 
5. cmd &> file : redirect output + error to file
6.  cmd 2>> foo : append error mesage to foo 
7. cmd 2> foo : Redirect error message to foo 
8. cmd <<< string : input a text string to cmd 
9. cmd << delim : imput from stdin with delimeter
10. cmd < file : read cmd input from file 
11. cmd >> file : Append output to file 

---

## Networking 
1. ifconfig : shall all interfaces and ips 
2. ifconfig -a : all interfaces including down 
3. ip a : another way to list interfaces 
4. netstat : open sockets and routing tables 
5. netstat -a : listening and non listening sockets 
6. ping host : send ICMP echo request to host 
7. whois domain : WHOIS info for domain
8. dig domain : DNS information for domain 
9. dig -x addr :Reverse DNS lookup on address
10. host domain : DNS IP address for domain 
11. wget LINK : dowload file from URL 
12. curl LINK : Display HTML source of URL 
13. ufw allow port : allow traffic on port 
14. ufw status : check firewall setting 
15. nmcli : manage network connectors 

---

## system information 
1. uname : show linux system information .
2. uname -a : detailed system information 
3. uname -r : kernal realse version .
4. uptime : system uptime and load 
5. date: currnal date and time 
6. shutdown : shutdown the system 
7. cat /etc/os-release : Linux distribution version 


