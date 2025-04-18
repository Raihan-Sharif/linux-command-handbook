# Linux File Permissions Guide

File permissions are a crucial part of Linux security, determining who can read, write, or execute files and directories. This guide explains how permissions work and how to manage them effectively.

## Understanding File Permissions

When you run `ls -l` in a directory, you'll see output like this:

```
-rwxr-xr-- 1 user group 4096 Oct 11 10:15 script.sh
```

### Permission String Breakdown

The first 10 characters represent the file type and permissions:

```
-rwxr-xr--
↑ ↑↑↑ ↑↑↑ ↑↑↑
│ │││ │││ │││
│ └┬┘ └┬┘ └┬┘
│  │   │   └── Others (Everyone else)
│  │   └────── Group (Members of the file's group)
│  └────────── Owner (User who owns the file)
└─────────────── File Type (- for file, d for directory)
```

### Permission Types

For each category (owner, group, others), there are three permission types:

- **r (read)**: 
  - For files: View content
  - For directories: List contents

- **w (write)**:
  - For files: Modify content
  - For directories: Create, delete, or rename files within

- **x (execute)**:
  - For files: Run as a program
  - For directories: Enter the directory

## Changing Permissions with `chmod`

The `chmod` command lets you modify file permissions in two ways: symbolic mode and numeric mode.

### Symbolic Mode

Symbolic mode uses letters to represent permissions and who they apply to:

- **Who**:
  - `u`: User/owner
  - `g`: Group
  - `o`: Others
  - `a`: All (equivalent to ugo)

- **Operation**:
  - `+`: Add permission
  - `-`: Remove permission
  - `=`: Set exact permission

- **Permission**:
  - `r`: Read
  - `w`: Write
  - `x`: Execute

#### Examples:

```bash
# Add execute permission for the owner
$ chmod u+x script.sh

# Remove write permission for group and others
$ chmod go-w file.txt

# Give everyone read permission
$ chmod a+r document.pdf

# Set specific permissions for each category
$ chmod u=rwx,g=rx,o=r file.txt
```

### Numeric Mode

Numeric mode uses numbers to represent permissions:

- **4**: Read (r)
- **2**: Write (w)
- **1**: Execute (x)

Add these values to set combined permissions:
- **7** = 4+2+1 = Read, Write, Execute (rwx)
- **6** = 4+2 = Read, Write (rw-)
- **5** = 4+1 = Read, Execute (r-x)
- **4** = Read only (r--)
- **3** = 2+1 = Write, Execute (-wx)
- **2** = Write only (-w-)
- **1** = Execute only (--x)
- **0** = No permissions (---)

The permission string is expressed as three digits: owner, group, others.

#### Examples:

```bash
# rwxr-xr-- (Owner: rwx, Group: r-x, Others: r--)
$ chmod 754 script.sh

# rw-r--r-- (Owner: rw-, Group: r--, Others: r--)
$ chmod 644 document.txt

# rwx------ (Owner: rwx, Group: ---, Others: ---)
$ chmod 700 private_script.sh
```

## Common Permission Patterns

### For Regular Files

- **644 (rw-r--r--)**:
  Standard permission for regular files. Owner can read and write, everyone else can only read.

- **640 (rw-r-----)**:
  More restricted. Owner can read and write, group can read, others have no access.

- **600 (rw-------)**:
  Private file. Only owner can read and write.

- **755 (rwxr-xr-x)**:
  For executable scripts. Owner has full control, others can read and execute.

- **775 (rwxrwxr-x)**:
  Collaborative scripts. Owner and group have full control, others can read and execute.

### For Directories

- **755 (rwxr-xr-x)**:
  Standard permission for directories. Owner has full control, others can list and access.

- **750 (rwxr-x---)**:
  More restricted. Owner has full control, group can list and access, others have no access.

- **700 (rwx------)**:
  Private directory. Only owner has access.

## Changing Ownership with `chown`

The `chown` command changes the owner and/or group of files and directories.

### Basic Syntax

```bash
chown [OPTIONS] [OWNER][:GROUP] FILE(s)
```

### Examples

```bash
# Change owner of file
$ chown user1 file.txt

# Change owner and group
$ chown user1:group1 file.txt

# Change only the group
$ chown :group1 file.txt

# Change recursively for all files in a directory
$ chown -R user1:group1 directory/
```

## Special Permissions

### Setuid (SUID)

When set on an executable file, the file runs with the permissions of the file owner, not the user who executes it.

```bash
# Set SUID (adds an 's' in the owner execute position)
$ chmod u+s executable_file

# Numeric mode (add 4000 to regular permissions)
$ chmod 4755 executable_file
```

### Setgid (SGID)

- On files: Runs with the permissions of the file's group
- On directories: New files created within inherit the directory's group

```bash
# Set SGID (adds an 's' in the group execute position)
$ chmod g+s file_or_directory

# Numeric mode (add 2000 to regular permissions)
$ chmod 2755 file_or_directory
```

### Sticky Bit

When set on a directory, users can only delete or rename files they own, even if they have write permissions on the directory.

```bash
# Set sticky bit (adds a 't' in the others execute position)
$ chmod +t directory

# Numeric mode (add 1000 to regular permissions)
$ chmod 1777 directory
```

## Checking Permissions

### Using `stat` Command

The `stat` command provides detailed information about file permissions:

```bash
$ stat file.txt
```

Example output:
```
  File: file.txt
  Size: 4096        Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d  Inode: 8531937     Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/   user)   Gid: ( 1000/   user)
Access: 2023-10-11 10:15:00.000000000 +0200
Modify: 2023-10-11 10:15:00.000000000 +0200
Change: 2023-10-11 10:15:00.000000000 +0200
 Birth: -
```

## Best Practices

1. **Principle of Least Privilege**: Grant only the permissions necessary for the user to perform their tasks
2. **Regular Audits**: Periodically review file permissions, especially for sensitive files
3. **Umask**: Set appropriate default permissions for new files using the `umask` command
4. **Security**: Be cautious with SUID/SGID permissions, as they can create security vulnerabilities if misused
5. **Directory Access**: Remember that to access a file in a directory, the user needs execute permission on that directory

## Example Permission Scenarios

### Web Server Files

```bash
# HTML/CSS/JS files (readable by all, writable only by owner)
$ chmod 644 website/*.html website/*.css website/*.js

# Web server config files (only accessible by owner and web server group)
$ chmod 640 config/*.conf
$ chown user:www-data config/*.conf

# Web content directory (group writable for collaborative development)
$ chmod 775 /var/www/html/
$ chown -R user:developers /var/www/html/
```

### Application Development

```bash
# Source code (collaborative development within team)
$ chmod 664 src/*.py
$ chown :developers src/

# Build scripts (executable by team members)
$ chmod 775 scripts/*.sh
$ chown :developers scripts/

# Private keys and credentials
$ chmod 600 keys/private.key
```

### Multi-user System

```bash
# Shared directory where users can share files
$ mkdir /shared
$ chmod 1775 /shared  # Sticky bit prevents users from deleting each other's files
$ chown root:users /shared

# Create user directories with appropriate permissions
$ mkdir /home/user1
$ chmod 750 /home/user1
$ chown user1:user1 /home/user1
```

Remember that understanding file permissions is essential for system security. Always check permissions when encountering access issues, and use the principle of least privilege when setting up new files and directories.
