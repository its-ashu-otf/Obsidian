### Silver Platter Machine

[https://tryhackme.com/room/silverplatter](https://tryhackme.com/room/silverplatter)


1. Pinging the target

```bash

ashu㉿kali ~/TryHackMe/SilverPlatter $ ping silverplatter.thm
PING silverplatter.thm (10.10.223.110) 56(84) bytes of data.
64 bytes from silverplatter.thm (10.10.223.110): icmp_seq=1 ttl=60 time=285 ms
64 bytes from silverplatter.thm (10.10.223.110): icmp_seq=2 ttl=60 time=244 ms
64 bytes from silverplatter.thm (10.10.223.110): icmp_seq=3 ttl=60 time=207 ms
^C
--- silverplatter.thm ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 207.271/245.229/284.809/31.675 ms

```

2. Scanning The Target

```bash
ashu㉿kali~ nmap silverplatter.thm -v -T5            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 07:54 EST
Initiating Ping Scan at 07:54
Scanning silverplatter.thm (10.10.205.70) [4 ports]
Completed Ping Scan at 07:54, 0.24s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 07:54
Scanning silverplatter.thm (10.10.205.70) [1000 ports]
Discovered open port 8080/tcp on 10.10.205.70
Discovered open port 22/tcp on 10.10.205.70
Discovered open port 80/tcp on 10.10.205.70
Completed SYN Stealth Scan at 07:54, 2.47s elapsed (1000 total ports)
Nmap scan report for silverplatter.thm (10.10.205.70)
Host is up (0.45s latency).
Not shown: 929 closed tcp ports (reset), 68 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8080/tcp open  http-proxy

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.82 seconds
           Raw packets sent: 1110 (48.816KB) | Rcvd: 933 (37.320KB)

```


```bash
ashu㉿kali~ nmap -A -p 22,80,8080 silverplatter.thm -v
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 07:55 EST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 07:55
Completed NSE at 07:55, 0.00s elapsed
Initiating NSE at 07:55
Completed NSE at 07:55, 0.00s elapsed
Initiating NSE at 07:55
Completed NSE at 07:55, 0.00s elapsed
Initiating Ping Scan at 07:55
Scanning silverplatter.thm (10.10.205.70) [4 ports]
Completed Ping Scan at 07:55, 0.25s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 07:55
Scanning silverplatter.thm (10.10.205.70) [3 ports]
Discovered open port 8080/tcp on 10.10.205.70
Discovered open port 80/tcp on 10.10.205.70
Discovered open port 22/tcp on 10.10.205.70
Completed SYN Stealth Scan at 07:55, 0.23s elapsed (3 total ports)
Initiating Service scan at 07:55
Scanning 3 services on silverplatter.thm (10.10.205.70)
Stats: 0:00:25 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 66.67% done; ETC: 07:56 (0:00:13 remaining)
Stats: 0:01:12 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 66.67% done; ETC: 07:57 (0:00:36 remaining)
Stats: 0:01:24 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 66.67% done; ETC: 07:57 (0:00:42 remaining)
Completed Service scan at 07:56, 88.54s elapsed (3 services on 1 host)
Initiating OS detection (try #1) against silverplatter.thm (10.10.205.70)
Initiating Traceroute at 07:56
Completed Traceroute at 07:56, 3.01s elapsed
Initiating Parallel DNS resolution of 1 host. at 07:56
Completed Parallel DNS resolution of 1 host. at 07:56, 0.07s elapsed
NSE: Script scanning 10.10.205.70.
Initiating NSE at 07:56
Completed NSE at 07:57, 6.36s elapsed
Initiating NSE at 07:57
Completed NSE at 07:57, 1.20s elapsed
Initiating NSE at 07:57
Completed NSE at 07:57, 0.00s elapsed
Nmap scan report for silverplatter.thm (10.10.205.70)
Host is up (0.21s latency).

PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 1b:1c:87:8a:fe:34:16:c9:f7:82:37:2b:10:8f:8b:f1 (ECDSA)
|_  256 26:6d:17:ed:83:9e:4f:2d:f6:cd:53:17:c8:80:3d:09 (ED25519)
80/tcp   open  http       nginx 1.18.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-title: Hack Smarter Security
|_http-server-header: nginx/1.18.0 (Ubuntu)
8080/tcp open  http-proxy
|_http-title: Error
| fingerprint-strings: 
|   FourOhFourRequest, HTTPOptions: 
|     HTTP/1.1 404 Not Found
|     Connection: close
|     Content-Length: 74
|     Content-Type: text/html
|     Date: Fri, 21 Feb 2025 12:55:31 GMT
|     <html><head><title>Error</title></head><body>404 - Not Found</body></html>
|   GenericLines, Help, Kerberos, LDAPSearchReq, LPDString, RTSPRequest, SMBProgNeg, SSLSessionReq, Socks5, TLSSessionReq, TerminalServerCookie: 
|     HTTP/1.1 400 Bad Request
|     Content-Length: 0
|     Connection: close
|   GetRequest: 
|     HTTP/1.1 404 Not Found
|     Connection: close
|     Content-Length: 74
|     Content-Type: text/html
|     Date: Fri, 21 Feb 2025 12:55:30 GMT
|_    <html><head><title>Error</title></head><body>404 - Not Found</body></html>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.95%I=7%D=2/21%Time=67B877C3%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,C9,"HTTP/1\.1\x20404\x20Not\x20Found\r\nConnection:\x20close\r
SF:\nContent-Length:\x2074\r\nContent-Type:\x20text/html\r\nDate:\x20Fri,\
SF:x2021\x20Feb\x202025\x2012:55:30\x20GMT\r\n\r\n<html><head><title>Error
SF:</title></head><body>404\x20-\x20Not\x20Found</body></html>")%r(HTTPOpt
SF:ions,C9,"HTTP/1\.1\x20404\x20Not\x20Found\r\nConnection:\x20close\r\nCo
SF:ntent-Length:\x2074\r\nContent-Type:\x20text/html\r\nDate:\x20Fri,\x202
SF:1\x20Feb\x202025\x2012:55:31\x20GMT\r\n\r\n<html><head><title>Error</ti
SF:tle></head><body>404\x20-\x20Not\x20Found</body></html>")%r(RTSPRequest
SF:,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nConn
SF:ection:\x20close\r\n\r\n")%r(FourOhFourRequest,C9,"HTTP/1\.1\x20404\x20
SF:Not\x20Found\r\nConnection:\x20close\r\nContent-Length:\x2074\r\nConten
SF:t-Type:\x20text/html\r\nDate:\x20Fri,\x2021\x20Feb\x202025\x2012:55:31\
SF:x20GMT\r\n\r\n<html><head><title>Error</title></head><body>404\x20-\x20
SF:Not\x20Found</body></html>")%r(Socks5,42,"HTTP/1\.1\x20400\x20Bad\x20Re
SF:quest\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(Gener
SF:icLines,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\
SF:r\nConnection:\x20close\r\n\r\n")%r(Help,42,"HTTP/1\.1\x20400\x20Bad\x2
SF:0Request\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(SS
SF:LSessionReq,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x
SF:200\r\nConnection:\x20close\r\n\r\n")%r(TerminalServerCookie,42,"HTTP/1
SF:\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nConnection:\x20
SF:close\r\n\r\n")%r(TLSSessionReq,42,"HTTP/1\.1\x20400\x20Bad\x20Request\
SF:r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(Kerberos,42
SF:,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nConnect
SF:ion:\x20close\r\n\r\n")%r(SMBProgNeg,42,"HTTP/1\.1\x20400\x20Bad\x20Req
SF:uest\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(LPDStr
SF:ing,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nC
SF:onnection:\x20close\r\n\r\n")%r(LDAPSearchReq,42,"HTTP/1\.1\x20400\x20B
SF:ad\x20Request\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
Uptime guess: 27.416 days (since Fri Jan 24 21:58:02 2025)
Network Distance: 5 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   86.79 ms  10.17.0.1
2   ... 4
5   205.05 ms silverplatter.thm (10.10.205.70)

NSE: Script Post-scanning.
Initiating NSE at 07:57
Completed NSE at 07:57, 0.00s elapsed
Initiating NSE at 07:57
Completed NSE at 07:57, 0.00s elapsed
Initiating NSE at 07:57
Completed NSE at 07:57, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 102.78 seconds
           Raw packets sent: 47 (2.870KB) | Rcvd: 28 (1.886KB)

```
### Rustscan Syntax

This too does what above nmap scan does 
```bash
ashu㉿kali~ rustscan -a silverplatter.thm -- -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
I don't always scan ports, but when I do, I prefer RustScan.

[~] The config file is expected to be at "/home/ashu/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.205.70:22
Open 10.10.205.70:80
Open 10.10.205.70:8080
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -A" on ip 10.10.205.70
Depending on the complexity of the script, results may take some time to appear.
Warning: Hit PCRE_ERROR_MATCHLIMIT when probing for service http with the regex '^HTTP/1\.1 \d\d\d (?:[^\r\n]*\r\n(?!\r\n))*?.*\r\nServer: Virata-EmWeb/R([\d_]+)\r\nContent-Type: text/html; ?charset=UTF-8\r\nExpires: .*<title>HP (Color |)LaserJet ([\w._ -]+)&nbsp;&nbsp;&nbsp;'
[~] Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 08:00 EST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 08:00
Completed NSE at 08:00, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 08:00
Completed NSE at 08:00, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 08:00
Completed NSE at 08:00, 0.00s elapsed
Initiating Ping Scan at 08:00
Scanning 10.10.205.70 [4 ports]
Completed Ping Scan at 08:00, 0.20s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 08:00
Scanning silverplatter.thm (10.10.205.70) [3 ports]
Discovered open port 80/tcp on 10.10.205.70
Discovered open port 22/tcp on 10.10.205.70
Discovered open port 8080/tcp on 10.10.205.70
Completed SYN Stealth Scan at 08:00, 0.22s elapsed (3 total ports)
Initiating Service scan at 08:00
Scanning 3 services on silverplatter.thm (10.10.205.70)
Stats: 0:00:30 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 66.67% done; ETC: 08:00 (0:00:15 remaining)
Stats: 0:00:32 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 66.67% done; ETC: 08:01 (0:00:16 remaining)
Completed Service scan at 08:00, 44.20s elapsed (3 services on 1 host)
Initiating OS detection (try #1) against silverplatter.thm (10.10.205.70)
Initiating Traceroute at 08:01
Completed Traceroute at 08:01, 3.01s elapsed
Initiating Parallel DNS resolution of 1 host. at 08:01
Completed Parallel DNS resolution of 1 host. at 08:01, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
NSE: Script scanning 10.10.205.70.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 08:01
Completed NSE at 08:01, 5.47s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 08:01
Completed NSE at 08:01, 1.20s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 08:01
Completed NSE at 08:01, 0.00s elapsed
Nmap scan report for silverplatter.thm (10.10.205.70)
Host is up, received echo-reply ttl 60 (0.20s latency).
Scanned at 2025-02-21 08:00:14 EST for 61s

PORT     STATE SERVICE    REASON         VERSION
22/tcp   open  ssh        syn-ack ttl 60 OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 1b:1c:87:8a:fe:34:16:c9:f7:82:37:2b:10:8f:8b:f1 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJ0ia1tcuNvK0lfuy3Ep2dsElFfxouO3VghX5Rltu77M33pFvTeCn9t5A8NReq3felAqPi+p+/0eRRfYuaeHRT4=
|   256 26:6d:17:ed:83:9e:4f:2d:f6:cd:53:17:c8:80:3d:09 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKecigNtiy6tW5ojXM3xQkbtTOwK+vqvMoJZnIxVowju
80/tcp   open  http       syn-ack ttl 60 nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-title: Hack Smarter Security
8080/tcp open  http-proxy syn-ack ttl 59
|_http-title: Error
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.1 404 Not Found
|     Connection: close
|     Content-Length: 74
|     Content-Type: text/html
|     Date: Fri, 21 Feb 2025 13:00:21 GMT
|     <html><head><title>Error</title></head><body>404 - Not Found</body></html>
|   GenericLines, Help, Kerberos, RTSPRequest, SMBProgNeg, SSLSessionReq, Socks5, TLSSessionReq, TerminalServerCookie: 
|     HTTP/1.1 400 Bad Request
|     Content-Length: 0
|     Connection: close
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 404 Not Found
|     Connection: close
|     Content-Length: 74
|     Content-Type: text/html
|     Date: Fri, 21 Feb 2025 13:00:20 GMT
|_    <html><head><title>Error</title></head><body>404 - Not Found</body></html>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.95%I=7%D=2/21%Time=67B878E4%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,C9,"HTTP/1\.1\x20404\x20Not\x20Found\r\nConnection:\x20close\r
SF:\nContent-Length:\x2074\r\nContent-Type:\x20text/html\r\nDate:\x20Fri,\
SF:x2021\x20Feb\x202025\x2013:00:20\x20GMT\r\n\r\n<html><head><title>Error
SF:</title></head><body>404\x20-\x20Not\x20Found</body></html>")%r(HTTPOpt
SF:ions,C9,"HTTP/1\.1\x20404\x20Not\x20Found\r\nConnection:\x20close\r\nCo
SF:ntent-Length:\x2074\r\nContent-Type:\x20text/html\r\nDate:\x20Fri,\x202
SF:1\x20Feb\x202025\x2013:00:20\x20GMT\r\n\r\n<html><head><title>Error</ti
SF:tle></head><body>404\x20-\x20Not\x20Found</body></html>")%r(RTSPRequest
SF:,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nConn
SF:ection:\x20close\r\n\r\n")%r(FourOhFourRequest,C9,"HTTP/1\.1\x20404\x20
SF:Not\x20Found\r\nConnection:\x20close\r\nContent-Length:\x2074\r\nConten
SF:t-Type:\x20text/html\r\nDate:\x20Fri,\x2021\x20Feb\x202025\x2013:00:21\
SF:x20GMT\r\n\r\n<html><head><title>Error</title></head><body>404\x20-\x20
SF:Not\x20Found</body></html>")%r(Socks5,42,"HTTP/1\.1\x20400\x20Bad\x20Re
SF:quest\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(Gener
SF:icLines,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\
SF:r\nConnection:\x20close\r\n\r\n")%r(Help,42,"HTTP/1\.1\x20400\x20Bad\x2
SF:0Request\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(SS
SF:LSessionReq,42,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x
SF:200\r\nConnection:\x20close\r\n\r\n")%r(TerminalServerCookie,42,"HTTP/1
SF:\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nConnection:\x20
SF:close\r\n\r\n")%r(TLSSessionReq,42,"HTTP/1\.1\x20400\x20Bad\x20Request\
SF:r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n")%r(Kerberos,42
SF:,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Length:\x200\r\nConnect
SF:ion:\x20close\r\n\r\n")%r(SMBProgNeg,42,"HTTP/1\.1\x20400\x20Bad\x20Req
SF:uest\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
TCP/IP fingerprint:
OS:SCAN(V=7.95%E=4%D=2/21%OT=22%CT=%CU=41632%PV=Y%DS=5%DC=T%G=N%TM=67B8791B
OS:%P=x86_64-pc-linux-gnu)SEQ(TI=Z%CI=Z)OPS(O1=M508ST11NW7%O2=M508ST11NW7%O
OS:3=M508NNT11NW7%O4=M508ST11NW7%O5=M508ST11NW7%O6=M508ST11)WIN(W1=F4B3%W2=
OS:F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M508NNSN
OS:W7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 0.000 days (since Fri Feb 21 08:00:59 2025)
Network Distance: 5 hops
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   76.02 ms  10.17.0.1
2   ... 4
5   206.01 ms silverplatter.thm (10.10.205.70)

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 08:01
Completed NSE at 08:01, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 08:01
Completed NSE at 08:01, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 08:01
Completed NSE at 08:01, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 61.19 seconds
           Raw packets sent: 92 (5.988KB) | Rcvd: 70 (4.644KB)



```



### Conclusion 

We found 3 Open ports
1. 22 SSH
2. 80 HTTP Server
3. 8080 Another Web Server Running


## Enumeration

### SSH (22)

SSH is Open let's check if it uses password authentication or key based authentication

```bash
ashu㉿kali ~ ssh root@silverplatter.thm
root@silverplatter.thm's password: 
```

### HTTP (80)

Running Dirsearch for Directory Eneumeration

```bash
ashu㉿kali~ dirsearch -u http://silverplatter.thm
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/ashu/reports/http_silverplatter.thm/_25-02-21_08-04-41.txt

Target: http://silverplatter.thm/

[08:04:41] Starting: 
[08:05:23] 301 -  178B  - /assets  ->  http://silverplatter.thm/assets/
[08:05:23] 403 -  564B  - /assets/
[08:05:48] 403 -  564B  - /images/
[08:05:48] 301 -  178B  - /images  ->  http://silverplatter.thm/images/
[08:05:53] 200 -   17KB - /LICENSE.txt
[08:06:13] 200 -  771B  - /README.txt

Task Completed


```

Checking for VHOSTS 

Running VHOST-Enumeration But we don't know the filter size so we will start with 1 as filter size

```bash
./vhost-fuzzer.sh silverplatter.thm  /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt http://silverplatter.thm 1

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://silverplatter.thm
 :: Wordlist         : FUZZ: /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
 :: Header           : Host: FUZZ.silverplatter.thm
 :: Header           : User-Agent: PENTEST
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 1
________________________________________________

11                      [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 226ms]
blog                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 221ms]
2006                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 236ms]
logo                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 241ms]
news                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 241ms]
privacy                 [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 242ms]
                        [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 243ms]
search                  [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 251ms]
spacer                  [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 251ms]
img                     [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 252ms]
full                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 269ms]
about                   [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 254ms]
index                   [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 277ms]
new                     [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 280ms]
crack                   [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 280ms]
images                  [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 281ms]
rss                     [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 284ms]
faq                     [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 290ms]
cgi-bin                 [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 290ms]
default                 [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 290ms]
home                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 294ms]
warez                   [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 296ms]
serial                  [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 314ms]
download                [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 314ms]
10                      [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 314ms]
contact                 [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 314ms]
12                      [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 315ms]
2005                    [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 198ms]
products                [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 213ms]
sitemap                 [Status: 200, Size: 14124, Words: 926, Lines: 346, Duration: 212ms]

```

So, When no response is coming the size is 14124 so lets change the filter size

```bash

ashu ㉿kali  ~/TryHackMe/SilverPlatter  ./vhost-fuzzer.sh silverplatter.thm  /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt http://silverplatter.thm 14124  

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://silverplatter.thm
 :: Wordlist         : FUZZ: /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
 :: Header           : Host: FUZZ.silverplatter.thm
 :: Header           : User-Agent: PENTEST
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 14124
________________________________________________

errata24                [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 234ms]
PressRoom               [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9803ms]
fox                     [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9679ms]
e4                      [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9406ms]
025                     [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9679ms]
support_off             [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9875ms]
spamstats               [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9888ms]
2151                    [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9978ms]
fur                     [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9840ms]
Shell                   [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 9992ms]
:: Progress: [35834/220560] :: Job [1/1] :: 197 req/sec :: Duration: [0:04:45] :: Errors: 0 ::

```



![[Pasted image 20250222191200.png]]