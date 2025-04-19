# Linux Everyday Commands Cheatsheet

A quick reference guide for the most commonly used Linux commands for daily operations.

## Navigation & File Management

| Command | Description | Example |
|---------|-------------|---------|
| `pwd` | Print working directory | `pwd` |
| `ls` | List directory contents | `ls -la` |
| `cd` | Change directory | `cd Documents` |
| `mkdir` | Create directory | `mkdir newdir` |
| `rmdir` | Remove empty directory | `rmdir emptydir` |
| `rm` | Remove files or directories | `rm file.txt`, `rm -rf dir` |
| `cp` | Copy files or directories | `cp file.txt backup/` |
| `mv` | Move/rename files or directories | `mv file.txt newname.txt` |
| `touch` | Create empty file or update timestamp | `touch newfile.txt` |
| `cat` | Display file contents | `cat file.txt` |
| `less` | View file contents page by page | `less largefile.log` |
| `head` | Display first lines of file | `head -n 10 file.txt` |
| `tail` | Display last lines of file | `tail -n 10 file.txt` |
| `find` | Search for files | `find . -name "*.txt"` |
| `grep` | Search text patterns | `grep "pattern" file.txt` |

## File Permissions

| Command | Description | Example |
|---------|-------------|---------|
| `chmod` | Change file permissions | `chmod 755 script.sh` |
| `chown` | Change file owner | `chown user:group file.txt` |
| `chgrp` | Change group ownership | `chgrp newgroup file.txt` |
| `umask` | Set default permissions | `umask 022` |

## File Operations

| Command | Description | Example |
|---------|-------------|---------|
| `ln` | Create links | `ln -s target link_name` |
| `du` | Estimate file space usage | `du -sh directory` |
| `df` | Report file system disk usage | `df -h` |
| `tar` | Archive files | `tar -czvf archive.tar.gz dir/` |
| `gzip` | Compress files | `gzip file.txt` |
| `gunzip` | Decompress files | `gunzip file.txt.gz` |
| `zip` | Package and compress files | `zip archive.zip file1 file2` |
| `unzip` | Extract zip archives | `unzip archive.zip` |
| `rsync` | Synchronize files/directories | `rsync -av source/ dest/` |

## Text Processing

| Command | Description | Example |
|---------|-------------|---------|
| `wc` | Count lines, words, bytes | `wc -l file.txt` |
| `sort` | Sort lines of text | `sort file.txt` |
| `uniq` | Report or omit repeated lines | `uniq sorted_file.txt` |
| `cut` | Remove sections from lines | `cut -d"," -f1 file.csv` |
| `paste` | Merge lines of files | `paste file1 file2` |
| `sed` | Stream editor for filtering/transforming | `sed 's/old/new/g' file.txt` |
| `awk` | Pattern scanning and processing | `awk '{print $1}' file.txt` |
| `tr` | Translate or delete characters | `cat file | tr 'a-z' 'A-Z'` |
| `diff` | Compare files line by line | `diff file1 file2` |

## Process Management

| Command | Description | Example |
|---------|-------------|---------|
| `ps` | Display current processes | `ps aux` |
| `top` | Dynamic real-time process viewer | `top` |
| `htop` | Interactive process viewer | `htop` |
| `kill` | Terminate processes | `kill -9 1234` |
| `killall` | Kill processes by name | `killall firefox` |
| `pgrep` | List processes by name | `pgrep nginx` |
| `pkill` | Signal processes by name | `pkill -15 nginx` |
| `nohup` | Run command immune to hangups | `nohup command &` |
| `bg` | Send processes to background | `bg %1` |
| `fg` | Bring processes to foreground | `fg %1` |
| `jobs` | List background jobs | `jobs` |

## System Information

| Command | Description | Example |
|---------|-------------|---------|
| `uname` | Print system information | `uname -a` |
| `hostname` | Show or set system hostname | `hostname` |
| `uptime` | Show how long system has been running | `uptime` |
| `date` | Display or set date and time | `date` |
| `cal` | Display calendar | `cal` |
| `w` | Show who is logged on and what they're doing | `w` |
| `whoami` | Print effective user ID | `whoami` |
| `id` | Print user and group IDs | `id` |
| `free` | Display amount of free/used memory | `free -h` |
| `lscpu` | Display CPU information | `lscpu` |
| `lsusb` | List USB devices | `lsusb` |
| `lspci` | List PCI devices | `lspci` |
| `lsblk` | List block devices | `lsblk` |
| `dmidecode` | Display hardware information | `sudo dmidecode` |

## Network Commands

| Command | Description | Example |
|---------|-------------|---------|
| `ifconfig` | Configure network interface | `ifconfig eth0` |
| `ip` | Show/manipulate routing, devices, etc. | `ip addr show` |
| `ping` | Send ICMP echo request | `ping google.com` |
| `traceroute` | Print the route packets take | `traceroute google.com` |
| `netstat` | Network statistics | `netstat -tuln` |
| `ss` | Socket statistics | `ss -tuln` |
| `dig` | DNS lookup utility | `dig google.com` |
| `nslookup` | Query DNS records | `nslookup google.com` |
| `host` | DNS lookup utility | `host google.com` |
| `whois` | Query whois servers | `whois domain.com` |
| `wget` | Download files from web | `wget https://example.com/file` |
| `curl` | Transfer data from/to server | `curl -O https://example.com/file` |
| `ssh` | OpenSSH client | `ssh user@server` |
| `scp` | Secure copy | `scp file.txt user@server:/path` |
| `sftp` | Secure FTP | `sftp user@server` |
| `iptables` | Administration tool for IPv4 filtering | `sudo iptables -L` |
| `tcpdump` | Dump network traffic | `sudo tcpdump -i eth0` |
| `nmap` | Network exploration tool | `nmap 192.168.1.1` |

## Disk and File System

| Command | Description | Example |
|---------|-------------|---------|
| `mount` | Mount a filesystem | `mount /dev/sdb1 /mnt` |
| `umount` | Unmount a filesystem | `umount /mnt` |
| `fdisk` | Partition table manipulator | `sudo fdisk -l` |
| `mkfs` | Build a Linux filesystem | `sudo mkfs.ext4 /dev/sdb1` |
| `fsck` | Check and repair filesystem | `sudo fsck /dev/sdb1` |
| `dd` | Convert and copy a file | `dd if=/dev/zero of=file bs=1M count=10` |
| `badblocks` | Search for bad blocks | `sudo badblocks -v /dev/sda` |

## Package Management (General)

| Command | Description | Example |
|---------|-------------|---------|
| `apt update` | Update package lists (Debian/Ubuntu) | `sudo apt update` |
| `apt install` | Install packages (Debian/Ubuntu) | `sudo apt install package` |
| `apt remove` | Remove packages (Debian/Ubuntu) | `sudo apt remove package` |
| `dnf install` | Install packages (RHEL/Fedora) | `sudo dnf install package` |
| `pacman -S` | Install packages (Arch) | `sudo pacman -S package` |

## System Control

| Command | Description | Example |
|---------|-------------|---------|
| `systemctl` | Control systemd services | `systemctl status nginx` |
| `service` | Run a System V init script | `service nginx status` |
| `reboot` | Reboot the system | `sudo reboot` |
| `shutdown` | Shutdown the system | `shutdown -h now` |
| `poweroff` | Power off the system | `sudo poweroff` |
| `journalctl` | Query systemd journal | `journalctl -u nginx` |

## User Environment

| Command | Description | Example |
|---------|-------------|---------|
| `echo` | Display a line of text | `echo "Hello World"` |
| `export` | Set environment variables | `export PATH=$PATH:/new/path` |
| `env` | Display environment variables | `env` |
| `alias` | Create command alias | `alias ll='ls -la'` |
| `history` | Command history | `history` |
| `clear` | Clear terminal screen | `clear` |
| `man` | Display manual pages | `man ls` |
| `info` | Display info pages | `info ls` |
| `which` | Locate a command | `which python` |
| `whereis` | Locate binary, source, manual | `whereis python` |
| `type` | Display command information | `type ls` |

## File Viewing and Editing

| Command | Description | Example |
|---------|-------------|---------|
| `nano` | Simple text editor | `nano file.txt` |
| `vim` | Vi improved text editor | `vim file.txt` |
| `emacs` | GNU Emacs text editor | `emacs file.txt` |
| `gedit` | GNOME text editor | `gedit file.txt` |
| `file` | Determine file type | `file document` |
| `stat` | Display file status | `stat file.txt` |
| `strings` | Print strings in binary files | `strings binary_file` |
| `hexdump` | Display file in hex | `hexdump -C file` |

## Compression

| Command | Description | Example |
|---------|-------------|---------|
| `bzip2` | Compress files using Burrows-Wheeler algorithm | `bzip2 file` |
| `bunzip2` | Decompress bzip2 files | `bunzip2 file.bz2` |
| `xz` | High-ratio compression | `xz file` |
| `unxz` | Decompress xz files | `unxz file.xz` |
| `7z` | 7-Zip file archiver | `7z a archive.7z directory/` |

## Time and Date

| Command | Description | Example |
|---------|-------------|---------|
| `date` | Display or set date and time | `date "+%Y-%m-%d %H:%M:%S"` |
| `time` | Time command execution | `time ls -la` |
| `timedatectl` | Control system time and date | `timedatectl status` |
| `ntpdate` | Set time via NTP | `sudo ntpdate pool.ntp.org` |

## Quick Tips

- **Command History**: Press Up/Down arrows to navigate through command history
- **Tab Completion**: Press Tab to auto-complete commands and file names
- **Command Cancellation**: Press Ctrl+C to cancel a running command
- **Terminal Clear**: Press Ctrl+L to clear terminal (same as `clear` command)
- **Copy/Paste**: Use Ctrl+Shift+C and Ctrl+Shift+V in most terminals
- **Background Process**: Add `&` at the end of a command to run it in background
- **View Command Manual**: Use `man command` to read the manual for any command
- **Command Substitution**: Use `$(command)` to use command output in another command
- **Piping**: Use `|` to send output of one command as input to another
- **Redirect Output**: Use `>` to redirect output to a file, `>>` to append
- **Redirect Input**: Use `<` to use file as input for a command
- **Multiple Commands**: Use `;` to run multiple commands sequentially
- **Conditional Execution**: Use `&&` (AND) and `||` (OR) for conditional command execution

## Getting Help

| Command | Description | Example |
|---------|-------------|---------|
| `--help` | Display command help | `ls --help` |
| `man` | Display manual page | `man ls` |
| `info` | Display info documentation | `info ls` |
| `whatis` | Display one-line manual description | `whatis ls` |
| `apropos` | Search manual pages | `apropos "list directory"` |
