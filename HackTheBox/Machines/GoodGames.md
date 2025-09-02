
# About GoodGames
GoodGames is an Easy linux machine that showcases the importance of sanitising user inputs in web applications to prevent SQL injection attacks, using strong hashing algorithms in database structures to prevent the extraction and cracking of passwords from a compromised database, along with the dangers of password re-use. It also highlights the dangers of using `render_template_string` in a Python web application where user input is reflected, allowing Server Side Template Injection (SSTI) attacks. Privilege escalation involves docker hosts enumeration and shows how having admin privileges in a container and a low privilege user on the host machine can be dangerous, allowing attackers to escalate privileges to compromise the system. 

## Categories

Top Level categories for GoodGames
- Vulnerability Assessment 
- Web Application 
- Enterprise Network

## Area of Interest

Learn about the technology and tools that can be found in GoodGames

- Virtualization 
- Security Tools 
- Authentication 
- Injections

## Vulnerabilities

Learn about the vulnerabilities and systems that can be found in GoodGames

SQL Injection Misconfiguration Server Side Template Injection (SSTI) 


## IP: `10.10.11.130`
# Walkthrough

## Reconnaissance 

1. Let's ping the target and check target is up or not.

```bash
ping goodgames.htb       
PING goodgames.htb (10.10.11.130) 56(84) bytes of data.
64 bytes from goodgames.htb (10.10.11.130): icmp_seq=1 ttl=63 time=77.7 ms
64 bytes from goodgames.htb (10.10.11.130): icmp_seq=2 ttl=63 time=77.7 ms
64 bytes from goodgames.htb (10.10.11.130): icmp_seq=3 ttl=63 time=77.6 ms
64 bytes from goodgames.htb (10.10.11.130): icmp_seq=4 ttl=63 time=76.5 ms
64 bytes from goodgames.htb (10.10.11.130): icmp_seq=5 ttl=63 time=76.1 ms
--- goodgames.htb ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4008ms
rtt min/avg/max/mdev = 76.122/77.117/77.692/0.672 ms
```

Target is up.

2. Now, let's scan the target and check for potential vulnerabilities 

```bash
snmap -sC -sV -T4 goodgames.htb
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-29 14:17 IST
Stats: 0:00:09 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 99.32% done; ETC: 14:17 (0:00:00 remaining)
Nmap scan report for goodgames.htb (10.10.11.130)
Host is up (0.076s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Werkzeug httpd 2.0.2 (Python 3.9.2)
|_http-title: GoodGames | Community and Store
|_http-server-header: Werkzeug/2.0.2 Python/3.9.2

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.62 seconds
```

Let's check if the request header has something of interest or not.

```bash
curl --head goodgames.htb
HTTP/1.1 200 OK
Date: Tue, 29 Apr 2025 08:27:22 GMT
Server: Werkzeug/2.0.2 Python/3.9.2
Content-Type: text/html; charset=utf-8
Content-Length: 85107
```

Nah, nothing of interest here

