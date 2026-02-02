###The Short Notes about the Kernel shell and usersace and init/systemd process####

####The core components of linux architecture######
1.Linux operating system has invented by linux torvald in 1991.
2.it is open source operating system unlike other os it is free to use 
3.it is multi user operating systems multiple users can use simultanously 

the component of linux are 
1.User
2.Application
3.Shell
4.Kernal 
5.Hardware

we have to remember as an ASK Application Shell Kernal and Hardware 
Meaning
1.Hardware : Physical Part 
2.Kernal : Controls hardware 
3.Shell : takes user commands 
4.Application : software you use 
5.USer : you 

what is Kernal :
1.kernal is the core (heart) of the linux operating system
2.It acts as a bridges between hardware and software 
3.it controls how software uses hardware 
4.linux kernal is the core part of the os that manages hardware resources and allows application to run safatly 
5.without kernal os cannot work 

why we need kernal ???
1.application cannot access hardware directy .
2.Kernal provides safe and controlled access to hardware .
3. it keeps the system stable and secure and efficient 

main functions of kernal 
1.process management 
2.memory management
3.file system management 
4.Device Management 
5.system calls 


Types of kernal :
1.Monoethic kernal 
2.Microkarnal 
3.Hybrid Kernak 


what is Hardware :
1.physical parts of the computer 
2.includes: CPU , RAM , Hard Disk , SSD , Keyboard , Mouse screen 
3.Hardware directly cannot used by appllications 

firstly user type any command on shell 
shell will read that command convert that command to kernal understandable form send it to kernal 
kernal reads that commands and execute it 


-----------
####Linux Booting process#######
1.Power Button Clicked ------> BIOS -----> Kernel------> Login Screen 
-when we press the power button .
electricty flows to mother board 
CPU wakes up 
-BIOS starts 
BIOS checks hardware (RAM , keyboard , disk)
This check is called POST 
Finds where Linux is installed 
-Bootloader (GROB)
BIOS loads GRUB 
GRUB shows Linux menu (if multiple OS)
GRUB loads Linux Kernal into memory 
-Kernal starts 
kernal takes control of the system 
detects hardware 
mount root file system
-systemd(PID 1) starts
kernal starts systemd 
systemd starts services
network 
SSH 
Login Services 
-Login Screen Appears 
GUI login or terminal login 


????Now Question Arises in our mind what is BIOS and GRUB???
-BIOS 
1.Basic Input Output System 
-BIOS is a small program stored on the motherboard 
-it runs before linux windows or any os starts 

why BIOS is needed??
-when your computer is off:
Ram is empty 
os is not loaded 
cpu doesnt know what to do 
BIOS is needed to wake up the system 


-GRUB 
-GRUB is a bootloader that loads the kernal into memory 
-BIOS only starts the computer and loads the bootloader it never loads the OS directly 
-it is the fisrt linux program that runs after BIOS 
-its main job is to load the linux kernal 
-BIOS cannot loads Linux directly 
-So GRUB helps 

---------------
###How Processess are created and Managed 
what is a process ?
-A process is a running program
eg:you type ls : ls stats running that is a process 
-what happens inside linux :
-shell is already running 
-shell creates a new process using fork()
-new process gets a PID 
-thats process runs the command using exec()
-kernal manages it untill it finishes 
-after commands completes ---->process ends 
-fork()------>creates process 
-exec()------>Runs program 

How kernal Manages process 
-kernal decides :
-which process runs on CPU 
-for how long 
-when to puase or resume 
This is called CPU scheduling 
thats how multitasking works 
process states (easy)
running - using cpu 
sleeping - waiting 
stopped - paused 
zombie - finished but not cleaned 


--------
#####what is the difference between system and init:
what is init:
-init is the fisrt process started by the kernal 
it has PID 1 
it starts system services
