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

````bash
# Create tar archive
$ tar -cf archive.tar files/

# Create compressed tar archive (gzip)
$ tar -czf archive.tar.gz files/

# Extract tar archive
$ tar -x


# Linux Commands for Developers (continued)

## Archive and Compression

```bash
# Create tar archive
$ tar -cf archive.tar files/

# Create compressed tar archive (gzip)
$ tar -czf archive.tar.gz files/

# Extract tar archive
$ tar -xf archive.tar

# Extract compressed tar archive
$ tar -xzf archive.tar.gz

# List contents of tar archive
$ tar -tf archive.tar

# Create zip archive
$ zip -r archive.zip directory/

# Extract zip archive
$ unzip archive.zip
````

## Debugging and Tracing

### strace (System Call Tracer)

```bash
# Trace system calls of a command
$ strace command

# Trace specific system calls
$ strace -e open,read command

# Attach to running process
$ strace -p process_id
```

### ltrace (Library Call Tracer)

```bash
# Trace library calls
$ ltrace command
```

### GDB (GNU Debugger)

```bash
# Debug a program
$ gdb ./program

# Run program with arguments in gdb
$ gdb --args ./program arg1 arg2

# Common GDB commands within the debugger:
# - run (r): Start the program
# - break (b) function/line: Set breakpoint
# - next (n): Execute next line
# - step (s): Step into function
# - continue (c): Continue execution
# - print (p) variable: Print variable value
# - backtrace (bt): Show call stack
# - quit (q): Exit GDB
```

## Package Building and Installation

### From Source

```bash
# Common procedure for building from source
$ ./configure
$ make
$ sudo make install

# Install to custom location
$ ./configure --prefix=/usr/local
$ make
$ sudo make install
```

### Debian/Ubuntu Packaging

```bash
# Build Debian package from source
$ dpkg-buildpackage -b

# Install local .deb package
$ sudo dpkg -i package.deb

# Fix dependencies after dpkg install
$ sudo apt-get install -f
```

### RPM-based Systems

```bash
# Build RPM package
$ rpmbuild -ba package.spec

# Install local RPM package
$ sudo rpm -ivh package.rpm
```

## Continuous Integration/Deployment Tools

### Jenkins CLI

```bash
# Download Jenkins CLI
$ wget http://jenkins-server:port/jnlpJars/jenkins-cli.jar

# Run Jenkins command
$ java -jar jenkins-cli.jar -s http://jenkins-server:port/ command
```

### GitHub Actions (Local Testing)

```bash
# Install act for local GitHub Actions testing
$ curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash

# Run GitHub Actions locally
$ act
```

## API Development and Testing

### cURL for API Testing

```bash
# Basic GET request
$ curl https://api.example.com/endpoint

# POST request with JSON data
$ curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' https://api.example.com/endpoint

# Authentication with token
$ curl -H "Authorization: Bearer token" https://api.example.com/endpoint

# Save response to file
$ curl -o response.json https://api.example.com/endpoint
```

### HTTPie (Modern HTTP Client)

```bash
# Install HTTPie
$ sudo apt install httpie

# Basic GET request
$ http https://api.example.com/endpoint

# POST with JSON
$ http POST https://api.example.com/endpoint key=value

# Authentication
$ http -a username:password https://api.example.com/endpoint
```

## Web Server Management

### Apache

```bash
# Start/stop/restart Apache
$ sudo systemctl start apache2
$ sudo systemctl stop apache2
$ sudo systemctl restart apache2

# Enable/disable site
$ sudo a2ensite site-name
$ sudo a2dissite site-name

# Enable/disable module
$ sudo a2enmod module-name
$ sudo a2dismod module-name

# Check configuration syntax
$ sudo apache2ctl configtest
```

### Nginx

```bash
# Start/stop/restart Nginx
$ sudo systemctl start nginx
$ sudo systemctl stop nginx
$ sudo systemctl restart nginx

# Test configuration syntax
$ sudo nginx -t

# Reload configuration without stopping
$ sudo nginx -s reload

# Enable/disable site
$ sudo ln -s /etc/nginx/sites-available/site /etc/nginx/sites-enabled/
$ sudo rm /etc/nginx/sites-enabled/site
```

## Cloud and Infrastructure Tools

### AWS CLI

```bash
# Configure AWS CLI
$ aws configure

# List S3 buckets
$ aws s3 ls

# Copy file to S3
$ aws s3 cp file.txt s3://bucket-name/

# List EC2 instances
$ aws ec2 describe-instances

# Create CloudFormation stack
$ aws cloudformation create-stack --stack-name mystack --template-body file://template.yaml
```

### Terraform

```bash
# Initialize working directory
$ terraform init

# Plan infrastructure changes
$ terraform plan

# Apply infrastructure changes
$ terraform apply

# Destroy infrastructure
$ terraform destroy
```

### Kubernetes (kubectl)

```bash
# View all pods
$ kubectl get pods

# Get pod details
$ kubectl describe pod pod-name

# Apply configuration
$ kubectl apply -f config.yaml

# View logs
$ kubectl logs pod-name

# Execute command in pod
$ kubectl exec -it pod-name -- /bin/bash

# View nodes
$ kubectl get nodes
```

## Security Tools for Developers

### File and Directory Encryption

```bash
# Encrypt a file with GPG
$ gpg -c file.txt

# Decrypt a file
$ gpg file.txt.gpg
```

### SSL/TLS

```bash
# Generate self-signed certificate
$ openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365

# View certificate details
$ openssl x509 -in cert.pem -text -noout

# Check server's certificate
$ openssl s_client -connect example.com:443
```

### Security Auditing

```bash
# Check open ports
$ sudo nmap -sS localhost

# Check for common vulnerabilities
$ sudo nmap -sV --script vuln example.com

# Check file permissions in web directory
$ find /var/www/html -type f -perm /o=w
```

## Performance Testing and Benchmarking

```bash
# HTTP benchmarking with ApacheBench
$ ab -n 1000 -c 100 https://example.com/

# Disk I/O performance
$ dd if=/dev/zero of=test bs=1G count=1 oflag=direct

# Memory bandwidth
$ mbw -t 0 1024

# Network performance
$ iperf -c server_ip
```

## Miscellaneous Developer Tools

### JSON Processing with jq

```bash
# Pretty-print JSON
$ cat file.json | jq .

# Extract specific field
$ cat file.json | jq '.field'

# Filter array
$ cat file.json | jq '.items[] | select(.status=="active")'
```

### Image Processing

```bash
# Resize image with ImageMagick
$ convert image.jpg -resize 50% resized.jpg

# Convert between formats
$ convert image.jpg image.png
```

### PDF Manipulation

```bash
# Combine PDFs with pdftk
$ pdftk file1.pdf file2.pdf cat output combined.pdf

# Extract pages
$ pdftk input.pdf cat 1-5 output output.pdf
```

Remember that many of these tools may need to be installed first using your distribution's package manager (apt, yum, etc.). Always refer to the documentation of individual tools for the most up-to-date and detailed information.
