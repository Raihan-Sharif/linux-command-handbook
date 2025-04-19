# Linux User Management

Managing users and groups is a fundamental part of Linux system administration. This guide covers the essential commands and concepts.

## User Management Commands

| Command | Description | Example |
|---------|-------------|---------|
| `useradd` | Create a new user | `sudo useradd username` |
| `usermod` | Modify user properties | `sudo usermod -a -G groupname username` |
| `userdel` | Delete a user | `sudo userdel username` |
| `passwd` | Change user password | `sudo passwd username` |
| `su` | Switch user | `su - username` |
| `sudo` | Execute command as another user | `sudo command` |
| `whoami` | Display current username | `whoami` |
| `id` | Display user/group IDs | `id username` |
| `users` | Show logged-in users | `users` |
| `w` | Show who is logged in and what they're doing | `w` |
| `last` | Show last logins | `last` |
| `finger` | User information lookup program | `finger username` |

## Creating & Modifying Users

### Create a New User

```bash
# Create user with default settings
sudo useradd newuser

# Create user with home directory
sudo useradd -m newuser

# Create user with specific home directory
sudo useradd -m -d /home/custom-dir newuser

# Create user with specific shell
sudo useradd -m -s /bin/bash newuser

# Create user with comment/full name
sudo useradd -m -c "Full Name" newuser

# Create user with specific UID
sudo useradd -m -u 1500 newuser

# Create user with expiry date
sudo useradd -m -e 2023-12-31 newuser
```

### Set/Change Password

```bash
# Set password for new user
sudo passwd username

# Change your own password
passwd
```

### Modify Existing Users

```bash
# Change username
sudo usermod -l newname oldname

# Change home directory
sudo usermod -d /new/home/dir username

# Change shell
sudo usermod -s /bin/zsh username

# Lock a user account
sudo usermod -L username

# Unlock a user account
sudo usermod -U username

# Set account expiry date
sudo usermod -e 2023-12-31 username

# Change user ID (UID)
sudo usermod -u 1001 username
```

### Delete Users

```bash
# Delete user
sudo userdel username

# Delete user and their home directory
sudo userdel -r username
```

## Group Management

| Command | Description | Example |
|---------|-------------|---------|
| `groupadd` | Create a new group | `sudo groupadd groupname` |
| `groupmod` | Modify a group | `sudo groupmod -n newname oldname` |
| `groupdel` | Delete a group | `sudo groupdel groupname` |
| `groups` | Show groups a user belongs to | `groups username` |
| `gpasswd` | Administer the /etc/group file | `sudo gpasswd -a username groupname` |

### Group Operations

```bash
# Create new group
sudo groupadd developers

# Add user to group
sudo usermod -a -G developers username
# OR
sudo gpasswd -a username developers

# Remove user from group
sudo gpasswd -d username developers

# Change group name
sudo groupmod -n new-name old-name

# Change group ID (GID)
sudo groupmod -g 1001 groupname

# Delete group
sudo groupdel groupname
```

## User Information & Configuration Files

| File | Description |
|------|-------------|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Encrypted passwords and account expiry |
| `/etc/group` | Group definitions |
| `/etc/gshadow` | Group passwords |
| `/etc/login.defs` | Default settings for user creation |
| `/etc/skel/` | Template files for new user home directories |

## Sudo Configuration

### Add User to Sudoers

```bash
# Add user to sudo group (Debian/Ubuntu)
sudo usermod -aG sudo username

# Add user to wheel group (RHEL/CentOS/Fedora)
sudo usermod -aG wheel username

# Edit sudoers file safely
sudo visudo
```

### Example Sudoers Entries

```bash
# Allow user to run any command without password
username ALL=(ALL) NOPASSWD: ALL

# Allow user to run specific commands without password
username ALL=(ALL) NOPASSWD: /bin/systemctl restart apache2

# Allow group to run any command with password
%developers ALL=(ALL) ALL
```

## User Limits and Resource Control

### Process & Resource Limits

```bash
# View user limits
ulimit -a

# Set maximum file size limit
ulimit -f 1000

# Set maximum number of processes
ulimit -u 50
```

### Configure User Limits in /etc/security/limits.conf

```bash
# Set hard and soft limits for a user
username soft nofile 4096
username hard nofile 10240

# Set limits for a group
@developers soft nproc 100
@developers hard nproc 200
```

## Monitoring Users

### Check Current User Sessions

```bash
# Who is logged in
who

# Detailed info about logged in users
w

# List last logins
last

# List failed login attempts
lastb
```

### Monitor User Activity

```bash
# View user's processes
ps -u username

# View all user processes
ps aux

# Monitor user processes in real-time
top -u username
```

## Best Practices

1. **Use Strong Passwords**: Enforce strong password policies.
2. **Least Privilege**: Give users only the permissions they need.
3. **Regular Audits**: Periodically review user accounts and permissions.
4. **Disable Unused Accounts**: Remove or disable accounts no longer in use.
5. **Set Password Expiry**: Force password changes at regular intervals.
6. **Use Groups**: Organize permissions with groups rather than individual users.
7. **Secure the Root Account**: Disable direct root login and use sudo instead.

## Additional Commands

```bash
# Create a system user (for services)
sudo useradd -r servicename

# Add user to multiple groups at once
sudo usermod -a -G group1,group2,group3 username

# Check password expiry information
sudo chage -l username

# Set password expiry rules
sudo chage -M 90 -m 7 -W 14 username

# Generate password hash for scripts
openssl passwd -6 -salt xyz mypassword
```

## Troubleshooting

### Common Issues

1. **Login Issues**: Check `/var/log/auth.log` or `/var/log/secure`
2. **Permission Problems**: Verify group membership with `groups` command
3. **Password Reset**: Boot to recovery mode or single user mode if root password is lost
4. **UID/GID Conflicts**: Use `find / -user UID -o -group GID` to find and fix conflicts
