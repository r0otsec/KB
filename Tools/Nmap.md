---
tags:
  - tool
  - linux
  - port-scanning
date: 2023-09-1
---

- Nmap is a common [[Port Scanning]] tool used to determine open ports and their services on target IPs and hostnames.
- Can be used to scan single machines, subnet ranges or hostnames.
- Automatically scans the top 1000 most common ports.
# Host Discovery

- `nmap 10.10.11.0/24 -sn | grep for | cut -d" " -f5`
# Scan IPs

- `-iL hosts.txt` - use file containing list of IPs
- `nmap 10.10.11.1 10.10.11.5` - scan non-consecutive IPs
- `nmap 10.10.11.1-5` - scan consecutive IPS
- `nmap 10.10.11.1` - scan single IP
# Port Definition

- `--top-ports=100` - define top ports
- `-p-` - scan all ports
- `-p22` - scan one port
- `-p22,80,443` - scan various ports
# Scan Types

- `-sT` - [[TCP]] connect scan
- `-sS` - TCP SYN scan
- `-sU` - [[UDP]] scan
# Version Identification

- `-sV` - version identification scan
- `-O` - detect OS
- `-A` - runs default scripts, version identification and OS detection
# Output

- `-oA` - output all formats (nmap, greppable, XML)
- `-oN` - output in Nmap format
- `-oG` - output in grep format
- `-oX` - output in XML format
# Scripts

- `-sC` - default scripts
- `--script [CATEGORY]` - specify category
- `--script [NAME],[NAME]` - run specific script
# Performance

- `--initial-rtt-timeout 50ms --max-rtt-timeout 100ms` - modify RTT times
- `--max-retries 0` - set number of retries sent
- `--min-rate 300` - set min rate (# of packets sent simultaneously)
- `-T[1-5]` - set timing template
# Evasion

- `-sA` - TCP ACK scan 
- `-D RND:5` - decoy scanning with 5 random IPS
- `-S` - specify source IP
- `--source-port 53` - perform scans from source port