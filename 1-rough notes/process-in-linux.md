# process-in-linux
---
Date: 02,Oct,2024
subject: process management in linux
field:[[linux]]
tags: #ps #top #kill #systemd #systemctl #journalctl

---

 - ANY PROGRAM THAT IS EXECUTED BECOMES A PROCESS
 - PID IS A UNIQUE NUMBER GIVEN TO PROCESS TO IDENTIFY THEM
 - PPID (Parent Process ID) is given to the process that started it
 - STATE is the current status of process (running , sleeping , stopped)
 - USER AND GID identify the owner and group of the process


# PROCESS STATE
- running = actively using cpu
- sleeping = waiting for an event
- stopped = paused 
- zombie = finished execution but still has an entry in process table (waiting for parent process to read exit status)

 now when the system is booting, kernal starts the first process called init process whose pid is 1, now many linux system uses systemd as their init program so systemd is the first process with pid of 1 and it does not have a PPID. you can confirm it by running `ps -p 1 -o pid,comm` 

### Process Termination

A process can terminate in several ways:
- Normal Termination = The process finishes execution and exits cleanly.
- Signal Termination = A process can receive signals that can terminate it (e.g., `SIGTERM`, `SIGKILL`).
- Exit Codes = Processes can return exit codes to indicate success or failure, which can be checked by the parent process.



### Process Priorities
- Changing Priorities = The priority of a process can be changed using the `nice` and `renice` commands, allowing users to adjust how much CPU time processes receive.
- Priority Levels = Ranges from -20 (highest priority) to 19 (lowest priority).
# SYSTEMD
In Linux, a service is a background process that performs specific functions for the system or for user applications. Services are often started during the boot process and run continuously, providing functionalities such as web serving, database management, and network services. They can operate without direct user interaction.

- services are defined by UNIT FILES hich contains configuration for how the service should behave
- unit files are located in */etc/systemd/system/* or */lib/systemd/system/*
### SERVICE STATE

 Active = The service is currently running.
 Inactive = The service is not running.
 Failed = The service has encountered an error and has stopped.

 SYSTEMCTL is used to control the status of the services
```bash

sudo systemctl start service-name = start a service
sudo systemctl stop service-name = stop a service
sudo systemctl status service-name = check status of service
sudo systemctl restart service-name = restart the service
sudo systemctl enable  service-name = start the service at boot
sudo systemctl disable service-name = disable it to start at boot
sudo systemctl enable --now service-name = start automatically on boot and now
sudo systemctl is-enabled service-name = check if service is enabled

sudo systemctl list-units --type=service --state=running = view active services
sudo systemctl list-unit-files --type=service = view all active/inactive service

journalctl -u service-name = show logs of a service
journalctl -u service-name -f = follow logs in real time

sudo systemctl mask  service-name = prevent it from starting  
sudo systemctl unmask service-name = unmask the masked service to enable it again

sudo systemctl daemon-reload = reload service without restarting after making change in unit file of a service

```

## TYPE OF PROCESS
Foreground process = the one which is in front of us
Background process = the one which is in background 

## PS (process status) displays info about running process
By default, it shows:
- PID = Process ID
- TTY = Terminal associated with the process
- TIME = Amount of CPU time consumed by the process
- CMD = The command that started the process
```bash

ps = will show running process in the current shell
ps -e = show all the active process
ps -ef = full format listing, shows more options
ps -u username/uid = show all processes running by the user
ps -g groupname/gid = show all process owned by the group
ps -p 1 -o comm=  => will show the name of process id

ps -eo pid,ppid,etcetc = print only the columns u want
useful options options
- PID = Process ID, a unique identifier for each running process.
- USER = The user that owns the process.
- CPU = Percentage of CPU usage.
- MEM = Percentage of memory usage.
- TTY = The terminal that controls the process.
- STAT = Process state (e.g., S for sleeping, R for running).
- START = When the process started.
- TIME = CPU time used by the process.
- COMMAND = The command that initiated the process

ps aux --sort=-%cpu = Sort by CPU usage (highest first) 
ps aux --sort=-%mem = Sort by memory usage (highest first)

pgrep process-name = give you pid of that process
pstree = shows running processes as a tree
```
### TOP 
- (table of process) shows a real-time view of running process 
##### available options inside top
k = kill
n = change no. of task
c = shows command absolute path
u = filter process by user
M = sort processes by memory
P = sort processces by cpu (default)
N = sort process by PID
T = sort by process running time
b = get a snapshot of current usage
top -b -n 1 = will give a single snapshot, n decides the number of snapshot
top -b -o %MEM -n 1 = by highest memory consumption

# KILL 
- kill is to kill a process
- KILL (signal)  (PID)

#### *SIGNALS*
kill -l = show all signal list

- SIGHUP = 1 = reload the process 
- SIGINT = 2 = equivalent to ctrl+c
- SIGKILL = 9 = forcefully kill process without giving it chance to clean up
- SIGTERM = 15 = graceful termination, request process to terminate gracefully
- SIGCONT = 18 = start the paused process
- SIGTOP = 19 =  pause the process without termination

`kill -9 firefox`
- like pgrep we have pkill which kills process using process name instead of process id
```bash
pkill firefox = kill firefox
pkill -i firefox = for case insenitivity
pkill -u myuser firefox = to kill firefox of myuser
pkill -9 firefox = to use specific kill signal
```
# NICE
NICE value shows the priority of a process
niceness scale goes from -20 to 19
the lower the number the higher the priority
-20 being the hight priority, 19 being lowest


nice -n 5 PID



