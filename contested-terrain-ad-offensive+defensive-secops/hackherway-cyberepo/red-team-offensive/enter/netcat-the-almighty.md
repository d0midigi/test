# Netcat: The Almighty

## Overview

Netcat is an incredibly versatile tool, often referred to as the "Swiss Army Knife" of hackers. At its core, Netcat is a utility that can read from and write to TCP and UDP ports. This means it can operate in two modes: client and server.

If you're unfamiliar with Netcat, take a moment to research it - it's a fundamental tool used in security assessments, red team engagements, penetration testing activities, and general hacking.

## Connecting to a TCP/UDP Port with Netcat

There are several scenarios where connecting to a TCP or UDP port using Netcat can be useful:

* Checking if a port is open or closed
* Reading a service banner from a port
* Manually interacting with a network service

```c
root2bt:~# nc -h
[v1.10-38]
connect to somewhere:    nc [-options] hostname port[s] [ports] ...
listen for inbound:    nc -l -p port [-options] [hostname] [port]
options:
        -c shell commands:        as '-e'; use /bin/sh to exec [dangerous!!]
        -e filename               program to exec after connect [dangerous!!]
        -b                        allow broadcasts
        -g gateway                source-routing hop point[s], up to 8
        -G num                    source-routing pointer: 4, 8, 12, ...
        -h                        this cruft
        -i secs                   delay interval for lines sent, ports scanned
        -k                        set keepalive option on socket
        -l                        listen mode, for inbound connects
        -n                        numeric-only IP addresses, no DNS
        -o file                   hex dump of traffic
        -p port                   local port number
        -r                        randomize local and remote ports
        -q secs                   quit after EOF on stdin and delay of secs
        -s addr                   local source address
        -T tos                    set Type of Service
        -t                        answer TELNET negotiation
        -u                        UDP mode
        -v                        verbose [use twice to be more verbose]
        -w secs                   timeout for connects and final net reads
        -z                        zero-I/O mode [used for scanning]

Port numbers can be individual or in ranges: lo-hi [inclusive];
Hyphens in port names must be backslash escaped (e.g., 'ftp\-data').
root@bt:~#        
                      
```

1. <mark style="color:purple;">**To connect to TCP port 21 on 192.168.9.220 and read from it, try the following:**</mark>

```c
root@bt:~# nc -vn 192.168.9.220 21
(UNKNOWN) [192.168.9.220] 21 [ftp] open
220-GuildFTPd FTP Server (c) 1997-2002
220-Version 0.999.14
220-Thanks!
220 Please enter your name:
```

Note that port 21 is open and advertises the FTP banner **220-GuildFTPd FTP Server (c) 1997-2002.** Press CTRL+C to exit Netcat.

2. <mark style="color:purple;">**To connect to port 80 on 192.168.9.240, send an HTTP HEAD request, and read the HTTP server banner, try the following:**</mark>

```c
root@bt:~# nc -vn 192.168.9.240 80
(UNKNOWN) [192.168.9.240] 80 [www] open
HEAD / HTTP/1.0

HTTP/1.1 200 OK
Date: Thur, 27 Mar 2025 05:53:08 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Sat, 11 Oct 2008 12:44:50 GMT
ETag: "78457-b8-a1b5f480"
Accept-Ranges: bytes
Content-Length: 184
Connection: close
Content-Type: text/html; charset=UTF-8

root@bt:~#
```

## Listening on a TCP/UDP Port with Netcat

Listening on a TCP/UDP port using Netcat is useful for network debugging client applications, or otherwise, receiving a TCP/UDP network connection. Try implementing a simple chat using Netcat. Please take note of your local IP address (mine is 192.168.8.74).







