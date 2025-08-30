⚙️ Managing Processes

Linux treats every task as a process. Managing processes ensures efficient use of system resources and stability.

📌 Process Types

Foreground Process → Runs in the terminal until completed.

Background Process → Runs in the background with &.

Daemon → Background service (e.g., sshd).

Zombie Process → Finished execution but still in process table.

Orphan Process → Parent terminated, adopted by init/systemd.

🔄 Process Lifecycle

Created (fork/exec)

Running

Waiting (I/O, resources)

Terminated (exit)

📊 Monitoring Processes

ps aux → Show all processes.

top / htop → Real-time monitoring.

pstree → Hierarchical process tree.

pgrep name → Find PID by process name.

Viewing Processes

ps (Process Status)

The ps command shows information about active processes.

# Show processes for the current user
ps

# Show all processes with full details
ps -ef

# Show processes in a tree structure

ps -ejH

Example output:

UID   PID  PPID  C STIME TTY          TIME CMD

root     1     0  0 Aug28 ?        00:00:04 systemd

root     2     0  0 Aug28 ?        00:00:00 kthreadd

top (Real-time Process Monitoring)

top displays running processes dynamically.

top

Inside top:

k → Kill a process

r → Renice (change priority)

q → Quit

htop (Enhanced top)

If installed, htop gives a more user-friendly interface.

htop

⏱️ Job Control

Run process in background: command &

Bring to foreground: fg %1

Resume background job: bg %1

List jobs: jobs

📉 Priorities & Scheduling

nice -n 10 command → Start process with priority.

renice -n 5 -p PID → Change priority of running process.

Controlling Processes

Starting a Process

# Run a program in the foreground

firefox

# Run a program in the background

firefox &

Checking Background Jobs

jobs

Bringing Job to Foreground

fg %1

Sending Job to Background

bg %1

❌ Killing Processes

kill -9 PID → Force kill.

pkill processname → Kill by name.

killall processname → Kill all instances.

🛠️ Systemd & Services

systemctl start service → Start service.

systemctl stop service → Stop service.

systemctl restart service → Restart service.

systemctl status service → Service status.

Killing Processes

kill

Kill a process by PID.

# Find PID

ps -ef | grep firefox

# Kill process with PID

kill 1234

# Force kill

kill -9 1234

pkill

Kill by process name.

pkill firefox

killall

Kill all instances of a process.

killall firefox

Process Priorities

Each process has a priority that determines CPU scheduling.

nice (Start process with priority)

# Start process with lower priority (10)

nice -n 10 firefox

renice (Change priority of running process)

# Change priority of PID 1234 to -5

renice -5 -p 1234

Daemons and Services

System services are managed via systemd.

# List all services

systemctl list-units --type=service

# Start a service

sudo systemctl start ssh

# Stop a service

sudo systemctl stop ssh

# Enable service to start on boot

sudo systemctl enable ssh

Monitoring Resource Usage

top or htop

Check CPU and memory usage.

pidstat

Monitor statistics per process.

pidstat 1

pmap

Show memory usage of a process.

pmap 1234

Example Workflow

Start a process in the background:

sleep 500 &

Check running processes:

ps -ef | grep sleep

Kill the process:

kill -9 <PID>

Verify it’s gone:

ps -ef | grep sleep

