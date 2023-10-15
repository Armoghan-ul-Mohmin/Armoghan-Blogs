---
title: "Nmap the Network Testing Tool"
date: 2023-10-15T19:57:16+05:00
image:
summary: "Pentesting with Nmap the Network Testing Tool (with Cheat Sheets)"
showReadingTime: true
tags: ['Nmap']
categories: ['Security']
series: ['kali']
series_order: 0
showComments : true
newsletter : true
draft : false
---
Nmap is a CLI based port scanner. As modern networking relies heavily on TCP ports, scanning these ports can expose valuable and critical data about a device on the network. These data can then be used to understand where vulnerabilities lie and how potential hackers can use them. Thus learning to port scan using Nmap is one of the first things a security researcher needs to grasp.

This guide contains the most valuable Nmap tricks/tips/commands that you can use for auditing/hacking a device on the network.

## 1. Target Specification
These are the basic commands to get started with nmap. It shows how different IPs can be targeted or filtered.
```bash
nmap 192.168.1.1                Scan a single IP
nmap 192.168.1.1 192.168.2.1    Scan specific IPs
nmap 192.168.1.1-254            Scan a range
nmap scanme.nmap.org            Scan a domain
nmap 192.168.1.0/24             Scan using CIDR notation
-iL     nmap -iL targets.txt    Scan targets from a file
-iR     nmap -iR 100            Scan 100 random hosts
--exclude   nmap --exclude 192.168.1.1      Exclude listed hosts
```

## 2. Scan Techniques
A port can be opened through many protocols (TCP/UDP) and can be put behind many types of firewall configurations. That’s why a port scan can be accomplished with multiple techniques. This is where knowledge of networking really comes in handy so that you know when to apply which type of port scans. The following are different techniques of scanning a port.

```bash
-sS     nmap 192.168.1.1 -sS    TCP SYN port scan (Default)
-sT     nmap 192.168.1.1 -sT    TCP connect port scan (Default without root privilege)
-sU     nmap 192.168.1.1 -sU    UDP port scan
-sA     nmap 192.168.1.1 -sA    TCP ACK port scan
-sW     nmap 192.168.1.1 -sW    TCP Window port scan
-sM     nmap 192.168.1.1 -sM    TCP Maimon port scan
```

## 3. Host Discovery
Sometimes you may want to scan a network to discover which hosts are up. After discovering the available hosts you can then scan the ports. The following presents different ways a host can be discovered on a network.

```bash
-sL     nmap 192.168.1.1-3 -sL          No Scan. List targets only
-sn     nmap 192.168.1.1/24 -sn         Disable port scanning. Host discovery only.
-Pn     nmap 192.168.1.1-5 -Pn          Disable host discovery. Port scan only.
-PS     nmap 192.168.1.1-5 -PS22-25,80  TCP SYN discovery on port x. Port 80 by default
-PA     nmap 192.168.1.1-5 -PA22-25,80  TCP ACK discovery on port x. Port 80 by default
-PU     nmap 192.168.1.1-5 -PU53        UDP discovery on port x. Port 40125 by default
-PR     nmap 192.168.1.1-1/24 -PR       ARP discovery on the local network
-n      nmap 192.168.1.1 -n             Never do DNS resolution
```

## 4. Port Specification
A computer usually serves ports from the range 0-65535. Scanning all ports is not usually feasible because scanning a single port can be time-consuming. You can specify which ports to scan reduce scan targets and get faster results. Ideally, you would want to scan ports where services are commonly opened. For example HTTP (80), HTTPS (443), SSH (22), 8080, etc.

```bash
-p          nmap 192.168.1.1 -p 21              Port scan for port x
-p          nmap 192.168.1.1 -p 21-100          Port range
-p          nmap 192.168.1.1 -p U:53,T:21-25,80 Port scan multiple TCP and UDP ports
-p-         nmap 192.168.1.1 -p-                Port scan all ports
-p          nmap 192.168.1.1 -p http,https      Port scan from service name
-F          nmap 192.168.1.1 -F                 Fast port scan (100 ports)
--top-ports nmap 192.168.1.1 --top-ports 2000   Port scan the top x ports
-p-65535    nmap 192.168.1.1 -p-65535           Leaving off initial port in range makes the scan start at port 1
-p0-        nmap 192.168.1.1 -p0-               Leaving off end port in range makes the scan go through to port 65535
```

## 5. Service and Version Detection
Detect OS version and more information about a service running on a port.
```bash
nmap 192.168.1.1 -A                         Enables OS detection, version detection, script scanning, and traceroute
nmap 192.168.1.1 -sV                        Attempts to determine the version of the service running on port
nmap 192.168.1.1 -sV --version-intensity 8  Intensity level 0 to 9. Higher number increases possibility of correctness
nmap 192.168.1.1 -sV --version-light        Enable light mode. Lower possibility of correctness. Faster
nmap 192.168.1.1 -sV --version-all          Enable intensity level 9. Higher possibility of correctness. Slower
```

## 6. OS Detection
```bash
nmap 192.168.1.1 -O                     Remote OS detection using TCP/IP stack fingerprinting
nmap 192.168.1.1 -O --osscan-limit      If at least one open and one closed TCP port are not found it will not try OS detection against host
nmap 192.168.1.1 -O --osscan-guess      Makes Nmap guess more aggressively
nmap 192.168.1.1 -O --max-os-tries 1    Set the maximum number x of OS  detection tries against a target
```

## 7. Timing and Performance
A port scan can be tricky in terms of time. A heavy port scan may raise the firewalls to filter all traffic coming from your PC. On the other hand, a slower scan may take a long time to be complete. You need to find the perfect balance for your case. The following will help to speed up/down your scan.

### Modify scan speed
```bash
-T0    nmap 192.168.1.1 -T0    Paranoid (0) Intrusion Detection System evasion
-T1    nmap 192.168.1.1 -T1    Sneaky (1) Intrusion Detection System evasion
-T2    nmap 192.168.1.1 -T2    Polite (2) slows down the scan to useless bandwidth and use fewer target  machine resources
-T3    nmap 192.168.1.1 -T3    Normal (3) which is default speed
-T4    nmap 192.168.1.1 -T4    Aggressive (4) speeds scans; assumes you are on a reasonably fast and reliable network
-T5    nmap 192.168.1.1 -T5    Insane (5) speeds scan; assumes you are on an extraordinarily fast network
```

### Parallelism/delays/timeouts
Add timeouts to your scans so that a single port doesn’t take too long to scan. You can also enable parallelism to scan multiple hosts together.
```bash
--host-timeout <time>           1s; 4m; 2h      Give up on target after this long

--min-rtt-timeout
--max-rtt-timeout
--initial-rtt-timeout <time>    1s; 4m; 2h      Specifies probe round trip time

--min-hostgroup
--max-hostgroup <size>          50; 1024        Parallel host scan group sizes

--min-parallelism
--max-parallelism <numprobes>   10; 1           Probe parallelization

--scan-delay
--max-scan-delay <time>         20ms; 2s; 4m;   Adjust delay between probes

--max-retries <tries>   3       Specify the maximum number of port scan probe retransmissions
--min-rate <number>     100     Send packets no slower than <numberr> per second
--max-rate <number>     100     Send packets no faster than <number> per second
```

## 8. Firewall Evasion and Spoofing
A modern web server sits behinds firewalls. Evading these firewalls can be hard when the firewalls are tightly configured with high security. However, you may be able to evade intrusion detection by firewalls by applying the following techniques.
```bash
-f          nmap 192.168.1.1 -f             Requested scan (including ping scans) use tiny fragmented IP packets.
                                            Harder for packet filters
--mtu       nmap 192.168.1.1 --mtu 32       Set your own offset size
-D          nmap -D 1.1.1.1,2.2.2.2         Send scans from spoofed IPs (decoys)
-S          nmap -S www.microsoft.com       Scan Facebook from Microsoft 
                    www.facebook.com        (-e eth0 -Pn may be required)
-g          nmap -g 53 192.168.1.1          Use given source port number

--proxies   nmap --proxies 192.168.1.1      Relay connections through HTTP/SOCKS4 proxies
nmap --data-length 200 192.168.1.1          Appends random data to sent packets
```

## 9. Output
Modify the output logged to the console by nmap. Alternatively, you can save the output to a file and then later resume a paused scan.
```bash
-v          nmap 192.168.1.1 -v                 Increase the verbosity level (use -vv or more for greater effect)
-oN         nmap 192.168.1.1 -oN normal.file    Normal output to the file normal.file
-oA         nmap 192.168.1.1 -oA results        Output in the three major formats at once
nmap 192.168.1.1 -oN file --append-output       Append a scan to a previous scan file
-d          nmap 192.168.1.1 -d                 Increase debugging level (use -dd or more for greater effect)
--reason    nmap 192.168.1.1 --reason           Display the reason a port is in a particular state, same output as -vv
--open      nmap 192.168.1.1 --open             Only show open (or possibly open) ports
--packet-trace  nmap 192.168.1.1 -T4 --packet-trace     Show all packets sent and received
--iflist        nmap --iflist                   Shows the host interfaces and routes
--resume        nmap --resume results.file      Resume a scan
```

That’s all the basic things about nmap you need to know. However, to be a master of nmap you need to be a master of networking. Learning the nitty-gritty details of TCP/UDP will give you a greater edge when scanning and put you far above the rest of the hackers. Until then keep practicing!