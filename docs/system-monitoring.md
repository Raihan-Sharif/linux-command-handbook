# System Monitoring Commands in Linux

This document covers various commands used for monitoring system resources, processes, and performance in Linux environments.

## Process Monitoring

### ps (Process Status)

Shows information about active processes.

```bash
# Show all processes
$ ps aux

# Format the output
$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem

# Show process tree
$ ps -ejH

# Show threads of a process
$ ps -Lf <pid>
```

### top

Interactive process viewer, updated in real-time.

```bash
# Basic usage
$ top

# Show specific user's processes
$ top -u username

# Batch mode (non-interactive output)
$ top -b -n 1
```

**Interactive commands within top:**
- Press `M` to sort by memory usage
- Press `P` to sort by CPU usage
- Press `k` to kill a process (enter PID)
- Press `r` to renice a process (change priority)
- Press `1` to show individual CPU cores
- Press `q` to quit

### htop

Enhanced version of top with a more user-friendly interface.

```bash
# Basic usage
$ htop

# Show processes of a specific user
$ htop -u username
```

### pgrep/pkill

Find or signal processes by name.

```bash
# Find PIDs of processes by name
$ pgrep firefox

# Kill processes by name
$ pkill firefox

# Send specific signal
$ pkill -9 firefox
```

## Memory Monitoring

### free

Displays amount of free and used memory in the system.

```bash
# Show memory in human-readable format
$ free -h

# Update continuously every 2 seconds
$ free -h -s 2

# Show memory in megabytes
$ free -m
```

### vmstat

Reports virtual memory statistics.

```bash
# Show statistics every 2 seconds
$ vmstat 2

# Show statistics with expanded memory information
$ vmstat -S M -s
```

### smem

Reports memory consumption with shared memory considered.

```bash
# Show processes sorted by unique memory usage
$ smem -k

# Show memory usage by user
$ smem -u
```

## Disk Usage and I/O

### df (Disk Free)

Shows disk space usage on mounted filesystems.

```bash
# Show in human-readable format
$ df -h

# Show filesystem type
$ df -T

# Show inode usage
$ df -i
```

### du (Disk Usage)

Shows disk usage of files and directories.

```bash
# Summarize directories in human-readable format
$ du -sh *
 
# Show the 10 largest directories in current location
$ du -sh * | sort -hr | head -10

# Total size of a directory
$ du -sh /path/to/directory
```

### iotop

Monitors I/O usage by processes (may need installation).

```bash
# Show only processes actually doing I/O
$ iotop -o

# Non-interactive batch mode
$ iotop -b -n 2
```

### iostat

Reports CPU and I/O statistics.

```bash
# Show extended statistics every 2 seconds
$ iostat -x 2

# Show statistics for specific device
$ iostat -xd /dev/sda 2
```

## Network Monitoring

### netstat

Displays network connections, routing tables, interface statistics.

```bash
# Show all listening ports
$ netstat -tuln

# Show all active connections
$ netstat -tuna

# Show statistics by protocol
$ netstat -s
```

### ss

Another utility to investigate sockets (replacement for netstat).

```bash
# Show all TCP sockets
$ ss -t

# Show listening sockets
$ ss -tuln

# Show processes using sockets
$ ss -tulnp
```

### iftop

Shows bandwidth usage on an interface (may need installation).

```bash
# Monitor specific interface
$ iftop -i eth0

# Don't resolve hostnames/port numbers
$ iftop -i eth0 -n
```

### tcpdump

Captures and displays network packets.

```bash
# Capture on specific interface
$ sudo tcpdump -i eth0

# Capture specific host traffic
$ sudo tcpdump host 192.168.1.1

# Capture specific port
$ sudo tcpdump port 80

# Write to file for later analysis
$ sudo tcpdump -w capture.pcap
```

## Load and Performance

### uptime

Shows system uptime and load averages.

```bash
$ uptime
```

Example output:
```
 14:30:05 up 3 days,  5:27,  2 users,  load average: 0.12, 0.17, 0.15
```

### w

Shows who is logged in and what they're doing.

```bash
$ w
```

### sar (System Activity Reporter)

Collects, reports, and saves system activity information.

```bash
# Show CPU usage in real-time every 2 seconds
$ sar 2

# Show memory usage
$ sar -r

# Show swap usage
$ sar -S

# Show disk I/O
$ sar -b

# Show network statistics
$ sar -n DEV
```

## CPU Information and Usage

### lscpu

Displays information about the CPU architecture.

```bash
$ lscpu
```

### mpstat

Reports processor-related statistics.

```bash
# Show stats for all CPUs every 2 seconds
$ mpstat -P ALL 2

# Report CPU utilization since boot
$ mpstat
```

### stress

Tool to impose load on systems for testing (may need installation).

```bash
# Stress CPU with 4 workers
$ stress --cpu 4

# Stress memory with 2 workers using 1GB each
$ stress --vm 2 --vm-bytes 1G
```

## Temperature and Hardware Monitoring

### sensors

Shows hardware monitoring sensors data.

```bash
# Show all sensor information
$ sensors

# Update detection
$ sudo sensors-detect
```

### lm-sensors

More comprehensive hardware monitoring.

```bash
# Install lm-sensors
$ sudo apt install lm-sensors

# Detect sensors
$ sudo sensors-detect

# Show sensor readings
$ sensors
```

### hddtemp

Shows hard drive temperature.

```bash
# Check temperature of specific drive
$ sudo hddtemp /dev/sda
```

## System Logs and Events

### journalctl

Query the systemd journal.

```bash
# Show all logs
$ journalctl

# Show logs for specific service
$ journalctl -u service-name

# Follow new messages
$ journalctl -f

# Show logs since yesterday
$ journalctl --since=yesterday

# Show kernel messages
$ journalctl -k
```

### dmesg

Prints the kernel ring buffer.

```bash
# Show all kernel messages
$ dmesg

# Human readable timestamps
$ dmesg -T

# Follow new messages
$ dmesg -w
```

### last

Shows listing of last logged-in users.

```bash
# Show login history
$ last

# Show reboot history
$ last reboot
```

## Container and Virtualization Monitoring

### docker stats

Shows live performance stats for Docker containers.

```bash
# Show all containers
$ docker stats

# Show specific container
$ docker stats container_id
```

### ctop

Top-like interface for container metrics (may need installation).

```bash
$ ctop
```

### kubectl top

Shows resource usage for Kubernetes pods and nodes.

```bash
# Show pod resource usage
$ kubectl top pods

# Show node resource usage
$ kubectl top nodes
```

## Comprehensive Monitoring Tools

### glances

Cross-platform system monitoring tool.

```bash
# Run in terminal
$ glances

# Run as web server
$ glances -w
```

### nmon

Systems administrator, tuner, and benchmark tool.

```bash
# Interactive mode
$ nmon

# Capture data to file
$ nmon -f -s 30 -c 60
```

### atop

Advanced system and process monitor.

```bash
# Interactive mode
$ atop

# Write to file
$ atop -w atop.log 30
```

## Graphical Monitoring Tools

### gnome-system-monitor

GUI system monitor for GNOME.

```bash
$ gnome-system-monitor
```

### ksysguard

GUI system monitor for KDE.

```bash
$ ksysguard
```

## Real-time Performance Monitoring Scripts

### One-liner for process memory usage

```bash
$ ps aux | awk '{print $2, $4, $11}' | sort -k2rn | head -10
```

### Watch command for real-time updates of any command

```bash
# Update df output every 2 seconds
$ watch -n 2 df -h

# Update free memory info with highlighted changes
$ watch -d -n 2 free -m
```

Remember that some of these tools may need to be installed using your distribution's package manager. The examples above should work on most Linux distributions, but there might be slight differences in output or available options.
