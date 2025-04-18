# Linux Commands for Developers

This document covers essential Linux commands specifically useful for software development, DevOps, and system administration tasks.

## Version Control Systems

### Git

```bash
# Initialize a repository
$ git init

# Clone a repository
$ git clone https://github.com/username/repository.git

# Check status of working tree
$ git status

# Add files to staging
$ git add filename
$ git add .

# Commit changes
$ git commit -m "Commit message"

# Push to remote repository
$ git push origin branch-name

# Pull from remote repository
$ git pull origin branch-name

# Create and checkout new branch
$ git checkout -b branch-name

# View commit history
$ git log
$ git log --oneline --graph
```

## Building and Compiling

### Make

```bash
# Run the default target
$ make

# Run a specific target
$ make target-name

# Clean build files
$ make clean
```

### GCC (GNU Compiler Collection)

```bash
# Compile a C program
$ gcc -o output_file source_file.c

# Compile with warnings and debugging info
$ gcc -Wall -g -o output_file source_file.c

# Compile C++ with g++
$ g++ -o output_file source_file.cpp
```

## Container and Virtualization

### Docker

```bash
# List running containers
$ docker ps

# List all containers (including stopped)
$ docker ps -a

# Pull an image
$ docker pull image-name:tag

# Run a container
$ docker run -d -p 8080:80 image-name

# Build an image from Dockerfile
$ docker build -t image-name:tag .

# Stop a container
$ docker stop container-id

# Remove a container
$ docker rm container-id

# List images
$ docker images
```

### Docker Compose

```bash
# Start services defined in docker-compose.yml
$ docker-compose up -d

# Stop services
$ docker-compose down

# View logs
$ docker-compose logs -f
```

## SSH and Remote Management

### SSH

```bash
# Connect to remote server
$ ssh username@hostname

# Connect with specific key
$ ssh -i /path/to/key.pem username@hostname

# Forward port (local to remote)
$ ssh -L local_port:destination:remote_port username@hostname

# Generate SSH key
$ ssh-keygen -t rsa -b 4096

# Copy SSH key to server
$ ssh-copy-id username@hostname
```

### SCP (Secure Copy)

```bash
# Copy file to remote server
$ scp file.txt username@hostname:/path/to/destination/

# Copy directory recursively
$ scp -r directory/ username@hostname:/path/to/destination/

# Copy from remote to local
$ scp username@hostname:/path/to/file.txt /local/path/
```

## Text Processing for Developers

### Sed (Stream Editor)

```bash
# Replace text in a file
$ sed 's/old-text/new-text/g' file.txt

# Replace text in-place
$ sed -i 's/old-text/new-text/g' file.txt

# Delete specific lines
$ sed '5d' file.txt               # Delete line 5
$ sed '/pattern/d' file.txt       # Delete lines matching pattern
```

### Awk

```bash
# Print specific columns
$ awk '{print $1, $3}' file.txt

# Sum the values in a column
$ awk '{sum += $1} END {print sum}' file.txt

# Filter rows by condition
$ awk '$3 > 100' file.txt
```

### Grep with Developer-Specific Examples

```bash
# Find all TODO comments in code
$ grep -r "TODO:" --include="*.py" .

# Find function definitions
$ grep -r "function " --include="*.js" .

# Count occurrences of a pattern
$ grep -c "ERROR" log.txt

# Show line numbers
$ grep -n "pattern" file.txt

# Search for whole words only
$ grep -w "class" *.java
```

## Process Management for Developers

### Managing Processes

```bash
# Run process in background
$ command &

# Bring process to foreground
$ fg %job_number

# List background jobs
$ jobs

# Run process that continues after logout
$ nohup command &

# Execute with low priority
$ nice -n 19 command
```

### Screen and Tmux

```bash
# Start a new screen session
$ screen

# Create a new window in screen
$ Ctrl+a c

# List windows in screen
$ Ctrl+a "

# Detach from screen
$ Ctrl+a d

# Reattach to screen
$ screen -r

# Start tmux
$ tmux

# Create new window in tmux
$ Ctrl+b c

# Split pane horizontally in tmux
$ Ctrl+b %

# Split pane vertically in tmux
$ Ctrl+b "

# Detach from tmux
$ Ctrl+b d

# Reattach to tmux
$ tmux attach
```

## Environment and Configuration

### Environment Variables

```bash
# Set environment variable temporarily
$ export VAR_NAME=value

# View environment variable
$ echo $VAR_NAME

# List all environment variables
$ env

# Add to PATH variable
$ export PATH=$PATH:/new/path
```

### Configuration Files

```bash
# Edit bash configuration
$ nano ~/.bashrc

# Apply changes to current session
$ source ~/.bashrc

# View system-wide configuration
$ cat /etc/environment
```

## Networking Tools for Developers

### Netstat and ss

```bash
# Show all listening ports
$ netstat -tuln
$ ss -tuln

# Show processes using ports
$ netstat -tulnp
```

### Web Development Tools

```bash
# Simple HTTP server (Python)
$ python -m http.server 8000

# Check HTTP headers
$ curl -I https://example.com

# Make API request and format JSON response
$ curl -s https://api.example.com | jq .
```

### Monitoring Network Traffic

```bash
# Monitor HTTP traffic
$ sudo tcpdump -i any port 80

# Continuous network statistics
$ netstat -i 1
```

## Performance Analysis

### System Resource Monitoring

```bash
# Continuous system monitoring
$ top
$ htop

# I/O operations monitoring
$ iostat -x 1

# CPU information
$ mpstat -P ALL 1
```

### Memory Analysis

```bash
# Memory usage details
$ free -h

# Process memory usage
$ ps aux --sort=-%mem | head

# Memory mapping of a process
$ pmap -x process_id
```

## Database Tools

### MySQL/MariaDB

```bash
# Connect to database
$ mysql -u username -p database_name

# Import SQL file
$ mysql -u username -p database_name < file.sql

# Export database
$ mysqldump -u username -p database_name > backup.sql
```

### PostgreSQL

```bash
# Connect to database
$ psql -U username database_name

# Run SQL script
$ psql -U username -d database_name -f script.sql

# Backup database
$ pg_dump -U username database_name > backup.sql
```

## Log Analysis

### Viewing and Analyzing Logs

```bash
# Real-time log view
$ tail -f /var/log/app.log

# Filter logs
$ grep "ERROR" /var/log/app.log

# Count occurrences by type
$ awk '{print $5}' /var/log/app.log | sort | uniq -c | sort -nr
```

### System Logs

```bash
# View system logs
$ journalctl

# Kernel messages
$ dmesg

# Follow specific service logs
$ journalctl -fu service-name
```

## Automation and Scripting

### Cron Jobs

```bash
# Edit user's crontab
$ crontab -e

# List user's crontab entries
$ crontab -l

# Example entry: run script every day at 3 AM
# 0 3 * * * /path/to/script.sh
```

### Shell Scripting Helpers

```bash
# Make script executable
$ chmod +x script.sh

# Check shell script syntax
$ shellcheck script.sh

# Debug shell script
$ bash -x script.sh
```

## File Permissions for Web Development

```bash
# Set permissions for web directories
$ find /var/www/html -type d -exec chmod 755 {} \;
$ find /var/www/html -type f -exec chmod 644 {} \;

# Give ownership to web server user
$ chown -R www-data:www-data /var/www/html
```

## Archive and Compression

```bash
# Create tar archive
$ tar -cf archive.tar files/

# Create compressed tar archive (gzip)
$ tar -czf archive.tar.gz files/

# Extract tar archive
$ tar -x