# Linux Command Handbook

A comprehensive guide to essential Linux commands for developers, system administrators, and DevOps professionals.

![Linux Terminal](https://img.shields.io/badge/Linux-Command%20Line-orange)
![Bash](https://img.shields.io/badge/Shell-Bash-lightgrey)
![Version](https://img.shields.io/badge/Version-1.0-blue)
![License](https://img.shields.io/badge/License-MIT-green)

## Introduction

This repository serves as a practical reference for Linux command-line operations, designed to help you navigate and master the Linux environment efficiently. Whether you're a beginner or an experienced user, this handbook provides clear examples and explanations for common tasks in development, DevOps, and system administration workflows.

## Table of Contents

- [Basic Navigation](#basic-navigation)
- [File Management](#file-management)
- [Viewing File Content](#viewing-file-content)
- [System Monitoring](#system-monitoring)
- [Searching & Finding](#searching--finding)
- [Networking](#networking)
- [File Permissions](#file-permissions)
- [Package Management](#package-management)
- [Developer Tools](#developer-tools)
- [Additional Resources](#additional-resources)

## Basic Navigation

### pwd (Print Working Directory)

Displays your current location in the filesystem.

```bash
$ pwd
```

**Output example:** `/home/username`

### ls (List)

Lists files and directories in the current location.

```bash
$ ls                # Basic listing
$ ls -l             # Detailed listing with permissions and sizes
$ ls -a             # Show all files (including hidden ones)
$ ls -lh            # Human-readable file sizes
```

**Output example:**

```
Documents/  Downloads/  Pictures/  file.txt
```

For more advanced usage, see [examples/ls-examples.md](examples/ls-examples.md)

### cd (Change Directory)

Navigate between directories.

```bash
$ cd /path/to/directory    # Navigate to specific path
$ cd ~                     # Go to home directory
$ cd ..                    # Go up one directory
$ cd -                     # Go to previous directory
```

## File Management

### touch

Create a new empty file or update a file's timestamp.

```bash
$ touch newfile.txt
$ touch -a file.txt        # Update access time only
```

### cp (Copy)

Copy files or directories.

```bash
$ cp source.txt destination.txt
$ cp source.txt /path/to/directory/
$ cp -r sourcedir/ destdir/  # Copy directory recursively
```

For detailed options, see [examples/cp-examples.md](examples/cp-examples.md)

### mv (Move/Rename)

Move or rename files and directories.

```bash
$ mv oldname.txt newname.txt        # Rename a file
$ mv file.txt /path/to/destination/ # Move a file
$ mv dir1/ dir2/                    # Move or rename directory
```

### rm (Remove)

Delete files and directories.

```bash
$ rm file.txt               # Remove a file
$ rm -i file.txt            # Interactive mode (asks before removing)
$ rm -r directory/          # Remove directory and contents
$ rm -rf directory/         # Force remove without confirmation (use with caution!)
```

### mkdir (Make Directory)

Create new directories.

```bash
$ mkdir new_directory
$ mkdir -p parent/child/grandchild  # Create parent directories as needed
```

## Viewing File Content

### cat

Display the entire content of a file.

```bash
$ cat file.txt
$ cat -n file.txt           # Show line numbers
```

### less

View file content one screen at a time (navigate with arrow keys).

```bash
$ less large_file.txt
```

**Navigation in less:**

- Press `q` to quit
- Press `/` to search
- Press `n` for next search result
- Press `g` to go to beginning of file
- Press `G` to go to end of file

### head / tail

View the beginning or end of a file.

```bash
$ head file.txt             # First 10 lines
$ head -n 5 file.txt        # First 5 lines
$ tail file.txt             # Last 10 lines
$ tail -n 20 file.txt       # Last 20 lines
$ tail -f log_file.txt      # Follow file updates in real-time
```

## System Monitoring

### top

Display real-time system process information.

```bash
$ top
$ top -u username           # Show only specific user's processes
```

### htop

An enhanced version of top with a more user-friendly interface (may need installation).

```bash
$ htop
```

### df (Disk Free)

Show disk space usage.

```bash
$ df -h                     # Human-readable sizes
```

### free

Display memory usage information.

```bash
$ free -h                   # Human-readable sizes
$ free -m                   # Show in megabytes
```

### ps (Process Status)

List running processes.

```bash
$ ps                        # Current user processes
$ ps aux                    # All processes with details
$ ps -ef                    # Full format listing
```

## Searching & Finding

### find

Search for files in directory hierarchies.

```bash
$ find /path -name "filename"
$ find . -type f -name "*.txt"        # Find text files in current directory
$ find /home -size +100M              # Find files larger than 100MB
$ find . -mtime -7                    # Files modified in the last 7 days
```

### grep

Search for patterns in files.

```bash
$ grep "search_term" file.txt
$ grep -i "case insensitive" file.txt # Ignore case
$ grep -r "text" directory/           # Recursive search
$ grep -v "exclude" file.txt          # Show lines that don't match
```

### which

Find the location of a command.

```bash
$ which python
$ which npm
```

## Networking

### ping

Check connectivity to a host.

```bash
$ ping google.com
$ ping -c 4 192.168.1.1     # Send only 4 packets
```

### ifconfig / ip

Display or configure network interfaces.

```bash
$ ifconfig                  # Show all interfaces
$ ip addr show              # Modern alternative to ifconfig
$ ip route                  # Show routing table
```

### netstat / ss

Display network connections and statistics.

```bash
$ netstat -tuln             # Show listening TCP/UDP ports
$ ss -tuln                  # Modern alternative to netstat
```

### curl / wget

Transfer data from or to a server.

```bash
$ curl https://example.com
$ wget https://example.com/file.zip
```

## File Permissions

### chmod

Change file permissions.

```bash
$ chmod 755 script.sh       # Numeric mode
$ chmod u+x file.sh         # Symbolic mode: add execute for user
$ chmod go-w file.txt       # Remove write for group and others
```

For detailed permission management, see [examples/permissions-guide.md](examples/permissions-guide.md)

### chown

Change file owner and group.

```bash
$ chown user:group file.txt
$ chown -R user:group directory/  # Recursive ownership change
```

## Package Management

### apt (Debian/Ubuntu)

```bash
$ sudo apt update                  # Update package lists
$ sudo apt install package_name    # Install a package
$ sudo apt upgrade                 # Upgrade all packages
$ apt search keyword               # Search for packages
```

### yum/dnf (RHEL/CentOS/Fedora)

```bash
$ sudo yum update
$ sudo yum install package_name
$ sudo dnf search keyword          # For newer versions
```

## Additional Resources

For more detailed information, check out the following sections:

- [File Management Guide](docs/file-management.md)
- [System Monitoring Commands](docs/system-monitoring.md)
- [Networking Tools](docs/networking.md)
- [Package Management](docs/package-management.md)
- [User Management](docs/user-management.md)
- [Developer Tools](docs/developer-tools.md)
- [Everyday Command Cheatsheet](cheatsheets/everyday-commands.md)
- [Advanced Commands](cheatsheets/advanced-commands.md)

## Contributing

Feel free to submit pull requests with improvements, additional commands, or better examples!

## License

This project is licensed under the MIT License - see the LICENSE file for details.
