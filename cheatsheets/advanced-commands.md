# Linux Advanced Commands Cheatsheet

This cheatsheet covers advanced Linux commands and techniques for power users, system administrators, and developers.

## Advanced File Operations

| Command          | Description                               | Example                                        |
| ---------------- | ----------------------------------------- | ---------------------------------------------- | -------------- | --------------- |
| `find` with exec | Find and execute command                  | `find . -name "*.log" -exec rm {} \;`          |
| `xargs`          | Build commands from standard input        | `find . -name "*.txt" \| xargs grep "pattern"` |
| `lsof`           | List open files                           | `lsof -i:80` (files using port 80)             |
| `dd`             | Convert and copy files                    | `dd if=/dev/urandom of=file bs=1M count=10`    |
| `rsync`          | Fast, versatile file copying              | `rsync -avz --progress source/ dest/`          |
| `inotifywait`    | Monitor filesystem events                 | `inotifywait -m -e modify /path/to/watch`      |
| `tee`            | Read from stdin and write to stdout/files | `command                                       | tee output.txt | grep "pattern"` |

## Advanced Text Processing

| Command          | Description                     | Example                                        |
| ---------------- | ------------------------------- | ---------------------------------------------- | --------------------------- |
| `awk`            | Pattern scanning and processing | `awk -F, '{sum+=$3} END {print sum}' file.csv` |
| `sed`            | Stream editor                   | `sed -i 's/old/new/g' file.txt`                |
| `cut` with regex | Extract using delimiter         | `echo "path=value"                             | cut -d= -f2`                |
| `join`           | Join lines from two files       | `join -t, -1 1 -2 1 file1.csv file2.csv`       |
| `comm`           | Compare sorted files            | `comm -12 file1 file2` (common lines)          |
| `tr`             | Translate characters            | `echo "text"                                   | tr '[:lower:]' '[:upper:]'` |
| `split`          | Split files into pieces         | `split -b 1G large_file chunk_`                |
| `csplit`         | Split files based on context    | `csplit file.txt /^Section/ {*}`               |
| `column`         | Format text as table            | `ls -l                                         | column -t`                  |

## Advanced Process Management

| Command   | Description                        | Example                          |
| --------- | ---------------------------------- | -------------------------------- | ---------------- |
| `nice`    | Run with modified priority         | `nice -n 10 command`             |
| `renice`  | Change priority of running process | `renice -n 10 -p 1234`           |
| `ionice`  | Set I/O scheduling class           | `ionice -c 2 -n 0 command`       |
| `timeout` | Run with time limit                | `timeout 10s command`            |
| `watch`   | Execute command periodically       | `watch -n 1 'ps aux              | grep apache'`    |
| `at`      | Schedule one-time job              | `echo "cmd"                      | at 2am tomorrow` |
| `batch`   | Execute when system load permits   | `echo "cmd"                      | batch`           |
| `time`    | Measure command execution time     | `time command`                   |
| `strace`  | Trace system calls and signals     | `strace -p 1234`                 |
| `ltrace`  | Library call tracer                | `ltrace ./program`               |
| `lsof`    | List open files by process         | `lsof -p 1234`                   |
| `fuser`   | Identify processes using files     | `fuser -v /var/log/syslog`       |
| `pstree`  | Display process tree               | `pstree -p`                      |
| `iotop`   | Monitor disk I/O                   | `sudo iotop`                     |
| `cgroups` | Control groups                     | `cgcreate -g cpu,memory:mygroup` |

## Advanced Networking

| Command             | Description                      | Example                                              |
| ------------------- | -------------------------------- | ---------------------------------------------------- |
| `ss`                | Socket statistics                | `ss -tunapl`                                         |
| `ip`                | Show/manipulate routing, devices | `ip route show`                                      |
| `iptables`          | IP filtering, NAT and more       | `iptables -L -n -v`                                  |
| `nftables`          | Next-gen packet filtering        | `nft list tables`                                    |
| `tcpdump`           | Analyze network traffic          | `tcpdump -i eth0 port 80`                            |
| `netcat (nc)`       | TCP/IP Swiss army knife          | `nc -l 8080` or `nc server 8080`                     |
| `socat`             | Multipurpose relay               | `socat TCP-LISTEN:8080,fork STDOUT`                  |
| `nmap`              | Network exploration              | `nmap -sS -p 1-65535 192.168.1.1`                    |
| `mtr`               | Traceroute and ping in one       | `mtr google.com`                                     |
| `iperf`             | Network performance testing      | `iperf -s` (server), `iperf -c 192.168.1.2` (client) |
| `curl` with options | Advanced data transfer           | `curl -v -X POST -d "data" https://api.example.com`  |
| `ssh` tunneling     | Secure tunneling                 | `ssh -L 8080:localhost:80 user@remote`               |
| `sshfs`             | Mount remote filesystems         | `sshfs user@server:/remote/path /local/path`         |
| `tcpflow`           | TCP flow recorder                | `tcpflow -c -i eth0 port 80`                         |
| `tshark`            | Command-line Wireshark           | `tshark -i eth0 -f "port 80"`                        |
| `bmon`              | Bandwidth monitor                | `bmon -p eth0`                                       |
| `iftop`             | Network usage                    | `iftop -i eth0`                                      |

## System Administration

| Command           | Description                   | Example                                 |
| ----------------- | ----------------------------- | --------------------------------------- |
| `systemctl`       | Control systemd               | `systemctl status nginx`                |
| `journalctl`      | Query systemd journal         | `journalctl -u nginx -f`                |
| `dmesg`           | Print kernel messages         | `dmesg -w` (follow)                     |
| `timedatectl`     | Control system time           | `timedatectl set-timezone UTC`          |
| `hostnamectl`     | Control system hostname       | `hostnamectl set-hostname newname`      |
| `localectl`       | Control system locale         | `localectl set-locale LANG=en_US.UTF-8` |
| `systemd-analyze` | Analyze boot time             | `systemd-analyze blame`                 |
| `logrotate`       | Rotate log files              | `logrotate -f /etc/logrotate.conf`      |
| `chroot`          | Run command with special root | `chroot /mnt /bin/bash`                 |
| `lsblk`           | List block devices            | `lsblk -f`                              |
| `blkid`           | Block device attributes       | `blkid /dev/sda1`                       |
| `tune2fs`         | Adjust filesystem parameters  | `tune2fs -l /dev/sda1`                  |
| `e2fsck`          | Check ext2/3/4 filesystem     | `e2fsck -f /dev/sda1`                   |
| `xfs_repair`      | Repair XFS filesystem         | `xfs_repair /dev/sda2`                  |
| `lvm`             | Logical Volume Manager        | `lvdisplay`, `vgdisplay`, `pvdisplay`   |
| `dmsetup`         | Device mapper setup           | `dmsetup info`                          |
| `dracut`          | Generate initramfs            | `dracut -f`                             |
| `ldconfig`        | Update shared library links   | `ldconfig`                              |

## Performance Analysis

| Command         | Description                   | Example                                      |
| --------------- | ----------------------------- | -------------------------------------------- |
| `vmstat`        | Virtual memory statistics     | `vmstat 1`                                   |
| `iostat`        | I/O statistics                | `iostat -x 1`                                |
| `mpstat`        | Multiprocessor statistics     | `mpstat -P ALL 1`                            |
| `sar`           | System activity reporter      | `sar -u 1 3` (CPU), `sar -r 1 3` (memory)    |
| `pidstat`       | Statistics for Linux tasks    | `pidstat -d 1`                               |
| `slabtop`       | Kernel slab cache information | `slabtop`                                    |
| `perf`          | Performance analysis          | `perf stat command`                          |
| `stress`        | Load and stress test          | `stress --cpu 8 --io 4 --vm 2 --timeout 60s` |
| `stress-ng`     | Advanced stress testing       | `stress-ng --cpu 8 --timeout 60s`            |
| `sysbench`      | Benchmarking tool             | `sysbench cpu run`                           |
| `lmbench`       | Suite of benchmarks           | `lmbench`                                    |
| `pmap`          | Process memory map            | `pmap -x 1234`                               |
| `valgrind`      | Memory debugging/profiling    | `valgrind --leak-check=full ./program`       |
| `sysdig`        | System exploration            | `sysdig proc.name=nginx`                     |
| `bcc/BPF tools` | Performance analysis tools    | `execsnoop`, `biolatency`, etc.              |

## Security Tools

| Command      | Description                  | Example                                           |
| ------------ | ---------------------------- | ------------------------------------------------- |
| `openssl`    | OpenSSL toolkit              | `openssl genrsa -out key.pem 2048`                |
| `ssh-keygen` | Generate SSH keys            | `ssh-keygen -t ed25519`                           |
| `gpg`        | GNU Privacy Guard            | `gpg -c file` (encrypt), `gpg file.gpg` (decrypt) |
| `chage`      | Change user password expiry  | `chage -l username`                               |
| `fail2ban`   | Ban IPs with failed auth     | `fail2ban-client status sshd`                     |
| `firewalld`  | Dynamic firewall manager     | `firewall-cmd --list-all`                         |
| `ufw`        | Uncomplicated firewall       | `ufw status`                                      |
| `lynis`      | Security auditing tool       | `lynis audit system`                              |
| `chkrootkit` | Check for rootkits           | `chkrootkit`                                      |
| `rkhunter`   | Rootkit hunter               | `rkhunter --check`                                |
| `aide`       | Advanced intrusion detection | `aide --check`                                    |
| `auditd`     | System audit daemon          | `auditctl -l` (list rules)                        |
| `ausearch`   | Search audit logs            | `ausearch -k authorization`                       |
| `checksec`   | Check binary security        | `checksec --file=/bin/ls`                         |
| `apparmor`   | Application security         | `apparmor_status`                                 |
| `selinux`    | Security-Enhanced Linux      | `sestatus`                                        |

## Advanced Shell Features

| Feature              | Description         | Example                                                           |
| -------------------- | ------------------- | ----------------------------------------------------------------- |
| Brace expansion      | Generate patterns   | `echo {1..5}`, `echo {a..e}`, `mkdir -p project/{src,docs,tests}` |
| Process substitution | Use output as file  | `diff <(ls dir1) <(ls dir2)`                                      |
| Here documents       | Input redirection   | `cat <<EOF > file.txt`                                            |
| Command substitution | Use command output  | `files=$(find . -name "*.txt")`                                   |
| Arithmetic expansion | Math operations     | `echo $((5+3))`                                                   |
| Parameter expansion  | String operations   | `${string:0:5}`, `${string//pattern/replacement}`                 |
| Redirection          | Advanced I/O        | `command >stdout.txt 2>stderr.txt`, `command &>/dev/null`         |
| Job control          | Process management  | `command &`, `fg %1`, `bg %2`, `jobs`                             |
| Coprocesses          | Bidirectional pipes | `coproc my_command`                                               |
| Named pipes          | Special FIFO files  | `mkfifo pipe; command1 > pipe & command2 < pipe`                  |

## Container & Virtualization

| Command        | Description                 | Example                                  |
| -------------- | --------------------------- | ---------------------------------------- |
| `docker`       | Container management        | `docker run -it ubuntu bash`             |
| `podman`       | Daemonless containers       | `podman run -it fedora bash`             |
| `kubectl`      | Kubernetes control          | `kubectl get pods`                       |
| `virsh`        | Manage virtual machines     | `virsh list --all`                       |
| `qemu`         | Machine emulator            | `qemu-system-x86_64 -hda image.qcow2`    |
| `virt-install` | Create virtual machines     | `virt-install --name=vm1 --ram=2048 ...` |
| `lxc`          | Linux containers            | `lxc-create -t download -n container1`   |
| `vagrant`      | VM development environments | `vagrant up`                             |

## Developer Tools

| Command             | Description                      | Example                                      |
| ------------------- | -------------------------------- | -------------------------------------------- | ----- |
| `git`               | Version control                  | `git clone https://github.com/user/repo.git` |
| `make`              | Build automation                 | `make -j8`                                   |
| `gdb`               | GNU debugger                     | `gdb ./program`                              |
| `nm`                | List symbols                     | `nm -D /lib/libc.so.6`                       |
| `objdump`           | Display object information       | `objdump -d binary`                          |
| `readelf`           | Display ELF file information     | `readelf -a binary`                          |
| `ldd`               | Print shared object dependencies | `ldd /bin/ls`                                |
| `strip`             | Discard symbols                  | `strip --strip-unneeded binary`              |
| `ctags`             | Generate tag files               | `ctags -R .`                                 |
| `cscope`            | Source code browser              | `cscope -R -b`                               |
| `doxygen`           | Documentation generator          | `doxygen Doxyfile`                           |
| `autoconf/automake` | Configure scripts                | `autoreconf -fi`                             |
| `cmake`             | Cross-platform building          | `cmake .`                                    |
| `clang-format`      | Code formatter                   | `clang-format -i file.cpp`                   |
| `patch`             | Apply patches                    | `patch -p1 < patch_file`                     |
| `diff`              | Generate patches                 | `diff -u original modified > patch_file`     |
| `strace`            | Trace system calls               | `strace -e open ls`                          |
| `ltrace`            | Trace library calls              | `ltrace -e malloc ls`                        |
| `addr2line`         | Convert addresses to file/line   | `addr2line -e binary 0x1234`                 |
| `xxd`               | Hex dump                         | `xxd file                                    | less` |
| `hexdump`           | Hex dump                         | `hexdump -C file                             | less` |

## Database Tools

| Command     | Description       | Example                                |
| ----------- | ----------------- | -------------------------------------- |
| `mysql`     | MySQL client      | `mysql -u user -p database`            |
| `psql`      | PostgreSQL client | `psql -U user database`                |
| `sqlite3`   | SQLite client     | `sqlite3 database.db`                  |
| `redis-cli` | Redis client      | `redis-cli`                            |
| `mongosh`   | MongoDB shell     | `mongosh "mongodb://localhost"`        |
| `pg_dump`   | PostgreSQL backup | `pg_dump -U user db > backup.sql`      |
| `mysqldump` | MySQL backup      | `mysqldump -u user -p db > backup.sql` |

## Advanced One-Liners

```bash
# Find largest files and directories
find . -type f -exec du -h {} \; | sort -rh | head -n 20

# Count lines of code recursively
find . -name "*.py" -type f -exec cat {} \; | wc -l

# Watch filesystem changes in real-time
watch -d -n 1 'df -h'

# Watch command output differences
watch -d -n 1 'ps aux | grep httpd'

# Find files modified in last 24 hours
find /path -mtime -1 -type f -print

# Search and replace in multiple files
find . -name "*.txt" -exec sed -i 's/old/new/g' {} \;

# Remove empty directories
find . -type d -empty -delete

# Kill processes matching a pattern
ps aux | grep process_name | grep -v grep | awk '{print $2}' | xargs kill -9

# Find files with SUID/SGID permissions
find / -type f \( -perm -4000 -o -perm -2000 \) -exec ls -la {} \; 2>/dev/null

# Monitor system calls of a process
strace -f -e trace=network -s 10000 -p $(pgrep process_name)

# Check SSL certificate expiration
echo | openssl s_client -servername example.com -connect example.com:443 2>/dev/null | openssl x509 -noout -dates

# Find duplicate files (by content)
find . -type f -exec md5sum {} \; | sort | uniq -w32 -d

# Find all listening ports and associated processes
sudo lsof -i -P -n | grep LISTEN

# Create a simple HTTP server
python3 -m http.server 8080

# Securely wipe disk data
sudo dd if=/dev/urandom of=/dev/sdX bs=4M status=progress

# Create a RAM disk
mkdir -p /mnt/ramdisk && mount -t tmpfs -o size=2G tmpfs /mnt/ramdisk

# Process accounting summary
sudo lastcomm username
```

## Customizing the Shell

### Advanced Prompt Customization

```bash
# Show git branch in prompt
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "

# Add timestamp to prompt
export PS1="\[\033[1;32m\][\$(date +%H:%M:%S)]\[\033[0m\] \u@\h:\w\$ "

# Show exit status of last command
export PS1="\[\033[1;36m\]\${?/#0/}\[\033[0m\]\u@\h:\w\$ "
```

### Advanced Aliases

```bash
# Directory navigation
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# Better defaults
alias grep='grep --color=auto'
alias ls='ls --color=auto'
alias ll='ls -la'
alias mkdir='mkdir -p'
alias df='df -h'
alias du='du -h'

# Safety nets
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Network
alias myip='curl ifconfig.me'
alias ports='netstat -tulanp'
alias listen='lsof -i -P | grep LISTEN'

# System
alias meminfo='free -m -l -t'
alias cpuinfo='lscpu'
alias df='df -h'
alias services='systemctl list-units --type=service'
```

## Troubleshooting Commands

| Command      | Description                 | Example                                 |
| ------------ | --------------------------- | --------------------------------------- |
| `dmesg`      | Kernel ring buffer          | `dmesg -T \| grep error`                |
| `journalctl` | System logs                 | `journalctl -xe`                        |
| `sysctl`     | Kernel parameters           | `sysctl -a \| grep net.ipv4.ip_forward` |
| `lspci`      | PCI devices                 | `lspci -vv`                             |
| `lsusb`      | USB devices                 | `lsusb -v`                              |
| `modprobe`   | Add/remove kernel modules   | `modprobe -r module_name`               |
| `lsmod`      | Show loaded modules         | `lsmod \| grep nvidia`                  |
| `smartctl`   | SMART disk monitoring       | `smartctl -a /dev/sda`                  |
| `sosreport`  | System diagnostic info      | `sosreport`                             |
| `hdparm`     | Hard drive parameters       | `hdparm -tT /dev/sda`                   |
| `badblocks`  | Check for bad blocks        | `badblocks -v /dev/sda`                 |
| `fsck`       | Filesystem check            | `fsck -y /dev/sda1`                     |
| `debugfs`    | Debug ext filesystem        | `debugfs /dev/sda1`                     |
| `efibootmgr` | Manipulate EFI boot manager | `efibootmgr -v`                         |

## Advanced System Administration

### Tuning System Performance

```bash
# Adjust swappiness (0-100, lower means less swapping)
sysctl vm.swappiness=10

# Increase file descriptors limit
ulimit -n 65535

# Show current file descriptors
cat /proc/sys/fs/file-nr

# Show memory allocation
cat /proc/meminfo

# Check dirty memory settings
sysctl -a | grep vm.dirty

# Set I/O scheduler
echo deadline > /sys/block/sda/queue/scheduler

# View CPU frequency settings
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

# Set CPU governor to performance
echo performance > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
```

### Managing System Resources

```bash
# Set CPU affinity for a process
taskset -cp 0,1 1234

# View current resource limits
ulimit -a

# Set process limits in /etc/security/limits.conf
* hard nofile 65535
* soft nofile 65535

# Check open file handles
lsof | wc -l

# List processes by memory usage
ps aux --sort=-%mem | head

# List processes by CPU usage
ps aux --sort=-%cpu | head
```

### Disk and Storage Operations

```bash
# Create RAID array
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sda1 /dev/sdb1

# Expand LVM volume
lvextend -L +10G /dev/mapper/vg-lv
resize2fs /dev/mapper/vg-lv

# Create encrypted volume
cryptsetup luksFormat /dev/sdb1
cryptsetup luksOpen /dev/sdb1 secure
mkfs.ext4 /dev/mapper/secure
mount /dev/mapper/secure /mnt/secure

# Zero out all empty disk space (for better compression)
dd if=/dev/zero of=/fillfile bs=1M; rm /fillfile

# Benchmark disk performance
dd if=/dev/zero of=test bs=1G count=1 oflag=dsync
```

### Advanced SSH Usage

```bash
# Jump host (ProxyJump)
ssh -J jumphost user@destination

# Port forwarding (local)
ssh -L 8080:localhost:80 user@remote

# Port forwarding (remote)
ssh -R 8080:localhost:80 user@remote

# Dynamic SOCKS proxy
ssh -D 1080 user@remote

# Keep SSH alive
ssh -o ServerAliveInterval=60 user@remote

# Agent forwarding
ssh -A user@remote

# X11 forwarding
ssh -X user@remote

# Use specific key
ssh -i ~/.ssh/special_key user@remote

# SSH config file tricks (~/.ssh/config)
Host bastion
    HostName bastion.example.com
    User jumpuser
    IdentityFile ~/.ssh/jump_key

Host internal
    HostName internal.local
    User internaluser
    ProxyJump bastion
    ForwardAgent yes
```

## Emergency Recovery

```bash
# Emergency kill of processes using high CPU
for i in $(ps aux | sort -nrk 3,3 | head -n 5 | awk '{print $2}'); do kill -9 $i; done

# Emergency free up disk space
du -hsx /* | sort -rh | head -n 10
find /var/log -type f -name "*.log" -exec truncate -s 0 {} \;
journalctl --vacuum-time=1d

# Reset forgotten root password from GRUB
# 1. At GRUB menu, press 'e' to edit
# 2. Find line with 'linux' or 'linux16', append 'init=/bin/bash'
# 3. Press Ctrl-X to boot
# 4. Mount / as read-write: mount -o remount,rw /
# 5. Change password: passwd root
# 6. Reboot: exec /sbin/init

# Emergency recovery with Live USB
# Mount filesystem
mount /dev/sda1 /mnt
# Chroot into system
mount --bind /dev /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys
chroot /mnt

# Recover deleted file (if still open)
lsof | grep '(deleted)'
# Then recover from /proc/[PID]/fd/[FD]
cp /proc/12345/fd/4 /path/to/recover/file
```

## Advanced Security Techniques

```bash
# Generate strong random password
openssl rand -base64 16

# Generate SSL certificate with SAN
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout server.key -out server.crt \
  -subj "/CN=example.com" \
  -addext "subjectAltName = DNS:example.com,DNS:www.example.com"

# Find setuid/setgid files
find / -type f -perm -04000 -ls 2>/dev/null
find / -type f -perm -02000 -ls 2>/dev/null

# Block IP with iptables
iptables -A INPUT -s 192.168.1.100 -j DROP

# Rate limit connections
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP

# Secure permissions recursively
find /path -type f -exec chmod 644 {} \;
find /path -type d -exec chmod 755 {} \;
```

## Advanced Git Commands

```bash
# Undo last commit but keep changes
git reset --soft HEAD^

# Rewrite history to modify author
git filter-branch --env-filter '
  if [ "$GIT_AUTHOR_EMAIL" = "old@example.com" ]; then
    export GIT_AUTHOR_EMAIL="new@example.com"
    export GIT_AUTHOR_NAME="New Name"
    export GIT_COMMITTER_EMAIL="new@example.com"
    export GIT_COMMITTER_NAME="New Name"
  fi
' -- --all

# Find commits that introduced regex
git log -p -G "regex pattern"

# Visualize commit history
git log --graph --oneline --all --decorate

# Clean up repository
git gc --aggressive --prune=now

# Show changes to a specific file over time
git log -p -- filename

# Find deleted file in history
git log --all --full-history -- **/filename.*
```

## Advanced Shortcuts and Key Bindings

| Shortcut           | Description                                  |
| ------------------ | -------------------------------------------- |
| `Ctrl+R`           | Reverse search command history               |
| `Ctrl+A`           | Go to beginning of line                      |
| `Ctrl+E`           | Go to end of line                            |
| `Ctrl+U`           | Cut from cursor to beginning of line         |
| `Ctrl+K`           | Cut from cursor to end of line               |
| `Ctrl+W`           | Cut word before cursor                       |
| `Alt+F`            | Move forward one word                        |
| `Alt+B`            | Move backward one word                       |
| `Ctrl+Z`           | Suspend process (resume with `fg`)           |
| `Ctrl+D`           | Exit shell (or EOF)                          |
| `Ctrl+L`           | Clear screen                                 |
| `Ctrl+T`           | Swap two characters                          |
| `Alt+T`            | Swap two words                               |
| `!!`               | Repeat last command                          |
| `!$`               | Last argument of previous command            |
| `!*`               | All arguments of previous command            |
| `!string`          | Execute last command starting with string    |
| `^string1^string2` | Replace string1 with string2 in last command |
