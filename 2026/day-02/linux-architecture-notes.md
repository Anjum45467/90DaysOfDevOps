Short Notes: Kernel, Shell, User Space, init / systemd

---

## Core Components of Linux Architecture

- Linux operating system was invented by **Linus Torvalds** in **1991**
- Linux is an **open-source operating system**
- It is **free to use**
- It is a **multi-user operating system**, where multiple users can work simultaneously

---

## Components of Linux

1. User  
2. Application  
3. Shell  
4. Kernel  
5. Hardware  

### Easy way to remember: **ASKUH**
- **A** – Application  
- **S** – Shell  
- **K** – Kernel  
- **U** – User  
- **H** – Hardware  

### Meaning:
- **Hardware** → Physical parts  
- **Kernel** → Controls hardware  
- **Shell** → Takes user commands  
- **Application** → Software you use  
- **User** → You  

---

## What is Kernel?

- Kernel is the **core (heart)** of the Linux operating system
- It acts as a **bridge between hardware and software**
- It controls how software uses hardware
- Linux kernel manages hardware resources and allows applications to run safely
- Without the kernel, the operating system **cannot work**

---

## Why Do We Need Kernel?

- Applications **cannot access hardware directly**
- Kernel provides **safe and controlled access** to hardware
- It keeps the system **stable, secure, and efficient**

---

## Main Functions of Kernel

1. Process management  
2. Memory management  
3. File system management  
4. Device management  
5. System calls  

---

## Types of Kernel

1. Monolithic Kernel  
2. Microkernel  
3. Hybrid Kernel  

---

## What is Hardware?

- Hardware means **physical parts of the computer**
- Includes:
- CPU  
- RAM  
- Hard Disk / SSD  
- Keyboard 
- Mouse  
- Screen  
- Hardware **cannot be used directly by applications**

---
## How a Command Works in Linux
 - User types a command in the shell
 - Shell reads the command
 - Shell converts it into kernel-understandable form
 - Shell sends it to the kernel
 - Kernel executes the command

---
 ## Linux Booting Process

 ### Boot Flow:

power Button -> BIOS -> GRUB -> Kernel -> systemd -> LOgin Screen 


### Step-by-step Explanation:

1. Power button is pressed  
2. Electricity flows to the motherboard and CPU wakes up  
3. **BIOS starts**
   - Checks hardware (RAM, keyboard, disk)
      - This check is called **POST**
      4. BIOS finds where Linux is installed  
      5. **Bootloader (GRUB)** is loaded
         - Shows Linux menu (if multiple OS)
	    - Loads Linux kernel into memory
	    6. **Kernel starts**
	       - Takes control of the system
	          - Detects hardware
		     - Mounts root file system
		     7. **systemd (PID 1) starts**
		        - Starts services like network, SSH, login
			8. Login screen appears (GUI or terminal)

			---

			## What is BIOS?

			- BIOS stands for **Basic Input Output System**
			- It is a **small program stored on the motherboard**
			- It runs **before Linux, Windows, or any OS**

			### Why BIOS is Needed?

			- When computer is OFF:
			  - RAM is empty
			    - OS is not loaded
			      - CPU does not know what to do
			      - BIOS is needed to **start the system**

			      ---

			      ## What is GRUB?

			      - GRUB is a **bootloader**
			      - It loads the **Linux kernel into memory**
			      - BIOS only loads the bootloader, **not the OS directly**
			      - GRUB is the **first Linux program** that runs after BIOS
			      - BIOS cannot load Linux directly, so **GRUB helps**

			      ---

			      ## How Processes Are Created and Managed

			      ### What is a Process?
			      - A process is a **running program**
			      - Example:
			        - You type `ls`
				  - `ls` starts running → this is a process

				  ### Process Creation Steps:

				  1. Shell is already running  
				  2. Shell creates a new process using `fork()`  
				  3. New process gets a **PID**
				  4. Process runs the command using `exec()`  
				  5. Kernel manages the process until it finishes  
				  6. After completion → process ends  

				  - `fork()` → Creates process  
				  - `exec()` → Runs program  

				  ---

				  ## How Kernel Manages Processes

				  Kernel decides:
				  - Which process runs on CPU  
				  - For how long  
				  - When to pause or resume  

				  This is called **CPU scheduling**  
				  This is how **multitasking** works

				  ### Process States:
				  - Running → using CPU  
				  - Sleeping → waiting  
				  - Stopped → paused  
				  - Zombie → finished but not cleaned  

				  ---

				  ## Difference Between init and systemd

				  ### What is init?
				  - init is the **first process started by the kernel**
				  - It has **PID 1**
				  - Starts system services
				  - Used in **old Linux systems**

				  ### How init Works:
				  - Starts services **one by one**
				  - Uses scripts
				  - If one service is slow, the whole boot is slow
				  - Like **standing in a single queue**

				  ---

				  ### What is systemd?
				  - systemd is a **modern replacement of init**
				  - It also has **PID 1**
				  - Faster and smarter

				  ### How systemd Works:
				  - Starts services **in parallel**
				  - Handles dependencies
				  - Faster boot
				  - Like **multiple queues at once**

				  ---

				  ## What systemd Does and Why It Matters

				  - systemd is the **first process started by the kernel**
				  - It controls everything running in the background
				  - It starts services like:
				    - Network
				      - SSH
				        - Docker
					  - Web servers
					  - It manages services:
					    - start
					      - stop
					        - restart
						  - enable (start at boot)
						    - disable (stop at boot)
						      - status

						      ---

						      ## What is PID, Daemon, and Service?

						      ### PID (Process ID)
						      - Every running process has a unique number
						      - That number is called **PID**
						      - PID helps the OS identify processes

						      ---

						      ### Daemon
						      - A daemon is a **background process**
						      - Runs without user interaction
						      - Examples:
						        - sshd
							  - httpd

							  ---

							  ### Service
							  - A service is a **managed daemon**
							  - Controlled by **systemd**

							  ---

							  ## Useful Process Commands

							  ```bash
							  ps        # show processes
							  top       # live process view
							  htop      # better than top
							  kill PID  # kill a process

