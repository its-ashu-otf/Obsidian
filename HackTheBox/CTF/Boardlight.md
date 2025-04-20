# About BoardLight

BoardLight is an easy difficulty Linux machine that features a `Dolibarr` instance vulnerable to [CVE-2023-30253](https://nvd.nist.gov/vuln/detail/CVE-2023-30253). This vulnerability is leveraged to gain access as `www-data`. After enumerating and dumping the web configuration file contents, plaintext credentials lead to `SSH` access to the machine. Enumerating the system, a `SUID` binary related to `enlightenment` is identified which is vulnerable to privilege escalation via [CVE-2022-37706]( https://nvd.nist.gov/vuln/detail/CVE-2022-37706) and can be abused to leverage a root shell.


# Walkthrough

IP:`10.10.11.11`
## Recon


1. Pinging the target

```bash
ping boardlight.htb
PING boardlight.htb (10.10.11.11) 56(84) bytes of data.
64 bytes from boardlight.htb (10.10.11.11): icmp_seq=1 ttl=63 time=64.7 ms
64 bytes from boardlight.htb (10.10.11.11): icmp_seq=2 ttl=63 time=63.7 ms
^C
--- boardlight.htb ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 63.658/64.197/64.736/0.539 ms

```

2. Let's scan the target

```bash

nmap -sC -sV -n boardlight.htb -oA nmap/boardlight
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-20 15:59 IST
Nmap scan report for boardlight.htb (10.10.11.11)
Host is up (0.064s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 06:2d:3b:85:10:59:ff:73:66:27:7f:0e:ae:03:ea:f4 (RSA)
|   256 59:03:dc:52:87:3a:35:99:34:44:74:33:78:31:35:fb (ECDSA)
|_  256 ab:13:38:e4:3e:e0:24:b4:69:38:a9:63:82:38:dd:f4 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.92 seconds

```

