## IP: `192.168.100.67`
## OS: Linux

```bash
┌──(rootkali)-[~]
└─# ping 192.168.100.67                                                                                                            1 ⨯
PING 192.168.100.67 (192.168.100.67) 56(84) bytes of data.
64 bytes from 192.168.100.67: icmp_seq=1 ttl=64 time=0.437 ms
64 bytes from 192.168.100.67: icmp_seq=2 ttl=64 time=0.388 ms
^C
--- 192.168.100.67 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1012ms
rtt min/avg/max/mdev = 0.388/0.412/0.437/0.024 ms

```

The target is **up**.

## NMAP Scan Results

```bash
┌──(rootkali)-[~]
└─# nmap -sC -sV -T4 target5.local -oN Target_5/nmap_scan_results.txt

Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-09 02:52 IST
Nmap scan report for target5.local (192.168.100.67)
Host is up (0.00026s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 ff:25:20:5d:bd:bf:22:43:8e:7a:66:b7:17:55:44:6b (RSA)
|   256 b3:7a:99:09:37:00:11:2e:0c:1d:33:30:6c:5a:18:53 (ECDSA)
|_  256 43:69:35:92:e2:e5:53:1f:9d:fd:fb:bf:54:81:b3:0f (ED25519)
MAC Address: 02:3C:9A:D3:D5:1B (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.72 seconds

```

Let's run bruteforce on SSH.

### Port 22 (SSH)

```bash

```