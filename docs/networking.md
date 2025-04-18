# Linux Networking Commands

This document covers essential networking commands in Linux for troubleshooting, configuration, monitoring, and analysis.

## Basic Connectivity

### ping

Tests connectivity to a network host.

```bash
# Basic ping
$ ping example.com

# Specify number of packets to send
$ ping -c 4 example.com

# Set packet size
$ ping -s 1500 example.com

# Set interval between packets (in seconds)
$ ping -i 0.2 example.com
```

### traceroute / tracepath

Shows the route packets take to a network host.

```bash
# Basic traceroute
$ traceroute example.com

# Use TCP SYN for probes
$ traceroute -T example.com

# Specify port number
$ traceroute -p 443 example.com

# Alternative command
$ tracepath example.com
```

### mtr (My Traceroute)

Combines functionality of ping and traceroute into a single network diagnostic tool.

```bash
# Run in terminal interface
$ mtr example.com

# Generate report
$ mtr --report example.com

# Run 10 pings per hop for report
$ mtr --report --count 10 example.com
```

## Network Configuration

### ifconfig

Displays or configures network interfaces (being replaced by `ip` but still common).

```bash
# Show all interfaces
$ ifconfig

# Show specific interface
$ ifconfig eth0

# Configure IP address
$ sudo ifconfig eth0 192.168.1.10 netmask 255.255.255.0

# Enable/disable interface
$ sudo ifconfig eth0 up
$ sudo ifconfig eth0 down
```

### ip

Modern command for showing and manipulating network devices, routing, etc.

```bash
# Show all addresses
$ ip addr show

# Show specific interface
$ ip addr show dev eth0

# Add IP address to interface
$ sudo ip addr add 192.168.1.10/24 dev eth0

# Delete IP address from interface
$ sudo ip addr del 192.168.1.10/24 dev eth0

# Enable/disable interface
$ sudo ip link set eth0 up
$ sudo ip link set eth0 down

# Show routing table
$ ip route show

# Add static route
$ sudo ip route add 10.0.0.0/24 via 192.168.1.1

# Show network statistics
$ ip -s link
```

### iwconfig

Configure wireless network interfaces.

```bash
# Show wireless interfaces
$ iwconfig

# Set wireless mode
$ sudo iwconfig wlan0 mode Managed

# Set ESSID
$ sudo iwconfig wlan0 essid "NetworkName"

# Set encryption key
$ sudo iwconfig wlan0 key 1234567890
```

### nmcli / nmtui

Command-line interface for NetworkManager.

```bash
# Show all connections
$ nmcli connection show

# Show active connections
$ nmcli connection show --active

# Show device status
$ nmcli device status

# Connect to a WiFi network
$ nmcli device wifi connect SSID-Name password wireless-password

# Text-based UI for NetworkManager
$ nmtui
```

## DNS Tools

### dig (Domain Information Groper)

DNS lookup utility.

```bash
# Basic lookup
$ dig example.com

# Look up specific record type
$ dig example.com MX
$ dig example.com NS

# Use specific DNS server
$ dig @8.8.8.8 example.com

# Short answer only
$ dig +short example.com
```

### nslookup

Query DNS servers for information.

```bash
# Basic lookup
$ nslookup example.com

# Query specific DNS server
$ nslookup example.com 8.8.8.8

# Look up specific record type
$ nslookup -type=MX example.com
```

### host

Simple DNS lookup utility.

```bash
# Basic lookup
$ host example.com

# Verbose output
$ host -v example.com

# Look up specific record type
$ host -t MX example.com
```

### whois

Query WHOIS domain registration information.

```bash
# Basic whois lookup
$ whois example.com

# Show specific field
$ whois example.com | grep "Registry Expiry Date"
```

## Network Scanning and Analysis

### nmap

Network exploration and security scanning.

```bash
# Basic scan
$ nmap 192.168.1.1

# Scan network range
$ nmap 192.168.1.0/24

# Scan specific ports
$ nmap -p 80,443 example.com

# Detect operating system
$ sudo nmap -O example.com

# Scan for services/versions
$ nmap -sV example.com

# Aggressive scan with all detection options
$ sudo nmap -A example.com
```

### netstat

Display network connections, routing tables, interface statistics.

```bash
# Show all active connections
$ netstat -a

# Show listening ports
$ netstat -l

# Show statistics by protocol
$ netstat -s

# Show processes using ports
$ netstat -tulnp
```

### ss

Socket statistics, modern replacement for netstat.

```bash
# Show all connections
$ ss

# Show listening ports
$ ss -l

# Show processes using sockets
$ ss -p

# Show TCP connections
$ ss -t

# Show UDP connections
$ ss -u
```

### tcpdump

Packet analyzer for network debugging.

```bash
# Capture packets on interface
$ sudo tcpdump -i eth0

# Capture specific host traffic
$ sudo tcpdump host 192.168.1.10

# Capture specific port
$ sudo tcpdump port 80

# Save capture to file
$ sudo tcpdump -w capture.pcap

# Read from capture file
$ tcpdump -r capture.pcap

# HTTP traffic only
$ sudo tcpdump -i eth0 port 80 and tcp
```

### wireshark / tshark

Graphical (wireshark) and command-line (tshark) network protocol analyzer.

```bash
# Start wireshark
$ wireshark

# Capture with tshark
$ sudo tshark -i eth0

# Capture with specific filter
$ sudo tshark -i eth0 -f "port 80"
```

## Bandwidth and Performance Testing

### iperf3

Network performance measurement tool.

```bash
# Run as server
$ iperf3 -s

# Run as client
$ iperf3 -c server_ip

# Run UDP test
$ iperf3 -c server_ip -u

# Set bandwidth for UDP test
$ iperf3 -c server_ip -u -b 100M
```

### speedtest-cli

Command-line interface for testing internet bandwidth.

```bash
# Run speed test
$ speedtest-cli

# Simple output
$ speedtest-cli --simple

# List servers
$ speedtest-cli --list
```

### bmon

Bandwidth monitor with multiple interfaces display.

```bash
$ bmon
```

## Network Configuration Files

### /etc/hosts

Local hostname to IP mapping.

```bash
# Example /etc/hosts file
127.0.0.1       localhost
192.168.1.10    server.local
```

### /etc/resolv.conf

DNS resolver configuration.

```bash
# Example /etc/resolv.conf file
nameserver 8.8.8.8
nameserver 8.8.4.4
search local
```

### /etc/network/interfaces (Debian/Ubuntu)

Network interface configuration.

```bash
# Example stanza for /etc/network/interfaces
auto eth0
iface eth0 inet static
    address 192.168.1.10
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

## Advanced Networking Tools

### netcat (nc)

Networking utility for reading from and writing to network connections.

```bash
# Connect to a server
$ nc example.com 80

# Listen on a port
$ nc -l 8080

# Port scanning
$ nc -zv example.com 20-30

# Transfer file
$ nc -l 1234 > received_file  # On receiver
$ nc 192.168.1.10 1234 < file_to_send  # On sender
```

### curl

Tool for transferring data with URLs.

```bash
# Basic GET request
$ curl http://example.com

# Download file
$ curl -O http://example.com/file.zip

# Send POST request
$ curl -X POST -d "data" http://example.com

# Send with headers
$ curl -H "Content-Type: application/json" http://example.com

# Include response headers
$ curl -i http://example.com
```

### wget

Non-interactive network downloader.

```bash
# Download file
$ wget http://example.com/file.zip

# Download recursively
$ wget -r http://example.com/

# Continue interrupted download
$ wget -c http://example.com/large_file.zip

# Background download
$ wget -b http://example.com/large_file.zip
```

### socat

Multipurpose relay for bidirectional data transfer.

```bash
# TCP port forwarding
$ socat TCP-LISTEN:8080,fork TCP:target-server:80

# Create a simple HTTP server
$ socat TCP-LISTEN:8080,reuseaddr,fork EXEC:"echo -e \"HTTP/1.1 200 OK\r\n\r\nHello World\""

# Unix domain socket to TCP
$ socat UNIX-LISTEN:/tmp/socket,fork TCP:localhost:22
```

## Firewall and Routing

### iptables

Administration tool for IPv4 packet filtering and NAT.

```bash
# List all rules
$ sudo iptables -L

# Allow incoming traffic on port
$ sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Block IP address
$ sudo iptables -A INPUT -s 192.168.1.100 -j DROP

# Save rules
$ sudo iptables-save > /etc/iptables.rules

# Restore rules
$ sudo iptables-restore < /etc/iptables.rules
```

### ufw (Uncomplicated Firewall)

Simplified firewall management.

```bash
# Enable ufw
$ sudo ufw enable

# Allow service
$ sudo ufw allow ssh
$ sudo ufw allow 80/tcp

# Deny service
$ sudo ufw deny telnet

# Show status
$ sudo ufw status verbose
```

### route

Show and manipulate IP routing table.

```bash
# Show routing table
$ route -n

# Add static route
$ sudo route add -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.1.1

# Delete route
$ sudo route del -net 192.168.2.0 netmask 255.255.255.0
```

## VPN and Remote Access

### ssh (Secure Shell)

Connect to remote machines securely.

```bash
# Connect to server
$ ssh user@example.com

# Specify port
$ ssh -p 2222 user@example.com

# Connect with identity file
$ ssh -i ~/.ssh/id_rsa user@example.com

# Port forwarding (local)
$ ssh -L 8080:localhost:80 user@example.com

# Port forwarding (remote)
$ ssh -R 8080:localhost:80 user@example.com
```

### ssh-keygen

Generate SSH key pairs.

```bash
# Generate RSA key
$ ssh-keygen -t rsa -b 4096

# Generate Ed25519 key (more secure)
$ ssh-keygen -t ed25519

# Generate key with specific file name
$ ssh-keygen -f ~/.ssh/mykey
```

### scp (Secure Copy)

Copy files between hosts securely.

```bash
# Copy local file to remote server
$ scp file.txt user@example.com:/path/

# Copy remote file to local system
$ scp user@example.com:/path/file.txt local_directory/

# Copy directory recursively
$ scp -r directory/ user@example.com:/path/
```

### rsync

Fast and versatile file copying tool.

```bash
# Sync local directory to remote
$ rsync -avz directory/ user@example.com:/path/

# Sync remote directory to local
$ rsync -avz user@example.com:/path/ local_directory/

# Dry run (show what would be transferred)
$ rsync -avzn directory/ user@example.com:/path/

# Use SSH with non-standard port
$ rsync -avz -e "ssh -p 2222" directory/ user@example.com:/path/
```

### OpenVPN

Open-source VPN solution.

```bash
# Connect to VPN server
$ sudo openvpn --config config.ovpn

# Run as daemon
$ sudo openvpn --daemon --config config.ovpn
```

## Troubleshooting Tools

### ethtool

Query or control network driver and hardware settings.

```bash
# Show interface information
$ sudo ethtool eth0

# Show driver information
$ sudo ethtool -i eth0

# Check link status
$ sudo ethtool eth0 | grep Link

# Control interface speed
$ sudo ethtool -s eth0 speed 1000 duplex full
```

### arp

Manipulate the system ARP cache.

```bash
# Show ARP cache
$ arp -a

# Add static ARP entry
$ sudo arp -s 192.168.1.100 00:11:22:33:44:55

# Delete ARP entry
$ sudo arp -d 192.168.1.100
```

### arping

Send ARP requests to a neighbor host.

```bash
# Send ARP request
$ arping -I eth0 192.168.1.1
```

### hostname

Show or set the system's hostname.

```bash
# Show hostname
$ hostname

# Show FQDN
$ hostname -f

# Show IP addresses
$ hostname -I
```

## Network Monitoring and Debugging

### iftop

Display bandwidth usage on an interface.

```bash
# Monitor specific interface
$ sudo iftop -i eth0

# Don't resolve hostnames/port numbers
$ sudo iftop -i eth0 -n
```

### nethogs

Monitor per-process network bandwidth usage.

```bash
# Monitor all interfaces
$ sudo nethogs

# Monitor specific interface
$ sudo nethogs eth0
```

### iptraf

Interactive IP LAN monitor.

```bash
$ sudo iptraf-ng
```

### lsof

List open files, including network connections.

```bash
# Show all network connections
$ sudo lsof -i

# Show specific port usage
$ sudo lsof -i :80

# Show connections for specific process
$ sudo lsof -i -P -n | grep firefox
```

### tcpflow

Capture and analyze TCP connections.

```bash
# Capture traffic on interface
$ sudo tcpflow -i eth0

# Capture specific port
$ sudo tcpflow -i eth0 port 80
```

This comprehensive guide covers most networking commands you'll need for daily operations, troubleshooting, and network management in Linux environments.
