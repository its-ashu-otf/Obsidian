## About RetroTwo

RetroTwo is an easy difficulty `Windows` machine, which highlights AD exploitation. Initial external enumeration reveals a publicly accessible `SMB Share` containing a `Microsoft Access Database` file, which is password protected. After cracking the password, the contents of the `accdb` file are accessible, enabling the retrieval of the `VBA` script inside, where `AD credentials` can be retrieved. Then, by abusing `pre-created computer accounts` , we gain access to a computer account with the GenericWrite privilege over another account, which, when leveraged, provides access to the system via `RDP` . Finally, exploiting the `RpcEptMapper` registry key results in privilege escalation to a system account.

## Machine Information

The User flag for this Box is located in a non-standard directory, `C:\` .

## OS: `Windows`

# Walk-through

## Enumeration

### Rustscan

```bash
 rustscan -a retro2.vl -- -A -O retrotwo_rustscan.txt
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/home/ashu/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.
Open 10.129.67.220:53
Open 10.129.67.220:88
Open 10.129.67.220:135
Open 10.129.67.220:139
Open 10.129.67.220:389
Open 10.129.67.220:464
Open 10.129.67.220:445
Open 10.129.67.220:593
Open 10.129.67.220:636
Open 10.129.67.220:3269
Open 10.129.67.220:3268
Open 10.129.67.220:3389
Open 10.129.67.220:5722
Open 10.129.67.220:9389
Open 10.129.67.220:49154
Open 10.129.67.220:49155
Open 10.129.67.220:49157
Open 10.129.67.220:49158
Open 10.129.67.220:49165
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -A -O retrotwo_rustscan.txt" on ip 10.129.67.220
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-02 23:42 IST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:42
Completed NSE at 23:42, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:42
Completed NSE at 23:42, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:42
Completed NSE at 23:42, 0.00s elapsed
Initiating Ping Scan at 23:42
Scanning 10.129.67.220 [4 ports]
Completed Ping Scan at 23:42, 0.10s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 23:42
Scanning retrotwo.htb (10.129.67.220) [19 ports]
Discovered open port 445/tcp on 10.129.67.220
Discovered open port 3389/tcp on 10.129.67.220
Discovered open port 139/tcp on 10.129.67.220
Discovered open port 53/tcp on 10.129.67.220
Discovered open port 135/tcp on 10.129.67.220
Discovered open port 88/tcp on 10.129.67.220
Discovered open port 49158/tcp on 10.129.67.220
Discovered open port 49154/tcp on 10.129.67.220
Discovered open port 3269/tcp on 10.129.67.220
Discovered open port 636/tcp on 10.129.67.220
Discovered open port 3268/tcp on 10.129.67.220
Discovered open port 9389/tcp on 10.129.67.220
Discovered open port 49155/tcp on 10.129.67.220
Discovered open port 464/tcp on 10.129.67.220
Discovered open port 49157/tcp on 10.129.67.220
Discovered open port 5722/tcp on 10.129.67.220
Discovered open port 49165/tcp on 10.129.67.220
Discovered open port 389/tcp on 10.129.67.220
Discovered open port 593/tcp on 10.129.67.220
Completed SYN Stealth Scan at 23:42, 0.16s elapsed (19 total ports)
Initiating Service scan at 23:42
Scanning 19 services on retrotwo.htb (10.129.67.220)
Completed Service scan at 23:43, 54.76s elapsed (19 services on 1 host)
Initiating OS detection (try #1) against retrotwo.htb (10.129.67.220)
Retrying OS detection (try #2) against retrotwo.htb (10.129.67.220)
Initiating Traceroute at 23:43
Completed Traceroute at 23:43, 0.08s elapsed
Initiating Parallel DNS resolution of 1 host. at 23:43
Completed Parallel DNS resolution of 1 host. at 23:43, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
NSE: Script scanning 10.129.67.220.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:43
NSE Timing: About 99.96% done; ETC: 23:43 (0:00:00 remaining)
Completed NSE at 23:44, 40.08s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:44
Completed NSE at 23:44, 2.27s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:44
Completed NSE at 23:44, 0.00s elapsed
Nmap scan report for retrotwo.htb (10.129.67.220)
Host is up, received echo-reply ttl 127 (0.069s latency).
Scanned at 2025-09-02 23:42:26 IST for 102s

PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 127 Microsoft DNS 6.1.7601 (1DB15F75) (Windows Server 2008 R2 SP1)
| dns-nsid:
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15F75)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2025-09-02 18:12:33Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: retro2.vl, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds  syn-ack ttl 127 Windows Server 2008 R2 Datacenter 7601 Service Pack 1 microsoft-ds (workgroup: RETRO2)
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 127
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: retro2.vl, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 127
3389/tcp  open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Service
| rdp-ntlm-info:
|   Target_Name: RETRO2
|   NetBIOS_Domain_Name: RETRO2
|   NetBIOS_Computer_Name: BLN01
|   DNS_Domain_Name: retro2.vl
|   DNS_Computer_Name: BLN01.retro2.vl
|   DNS_Tree_Name: retro2.vl
|   Product_Version: 6.1.7601
|_  System_Time: 2025-09-02T18:13:26+00:00
|_ssl-date: 2025-09-02T18:14:06+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=BLN01.retro2.vl
| Issuer: commonName=BLN01.retro2.vl
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2025-09-01T18:04:23
| Not valid after:  2026-03-03T18:04:23
| MD5:   1c3e:39e7:e457:44b6:16aa:cec4:ea16:c928
| SHA-1: 23f9:ec6e:4335:6a73:8085:d812:6968:3c15:4d72:247d
| -----BEGIN CERTIFICATE-----
| MIIC4jCCAcqgAwIBAgIQO623ld+LN5JKjTUAbcEyeTANBgkqhkiG9w0BAQUFADAa
| MRgwFgYDVQQDEw9CTE4wMS5yZXRybzIudmwwHhcNMjUwOTAxMTgwNDIzWhcNMjYw
| MzAzMTgwNDIzWjAaMRgwFgYDVQQDEw9CTE4wMS5yZXRybzIudmwwggEiMA0GCSqG
| SIb3DQEBAQUAA4IBDwAwggEKAoIBAQDNtyeP19qui68pXxk2DNi5r3fylDsp6bqM
| iKYWQPFNpQzRp9qHoM8AdYi7YR+HSitdVbY8SM8sdUwzf6riDoNO2CJ2prZzZttS
| zAzaAdyOpwfRJlGmQCZs1clZaltJKieDh7WY02rRCqZj4OLkh5FzSjtfBzgqSfYd
| vBIIL7RfT+vfk0+YLuQRzEflOXbr0zi1ynbgLWJPDYO/+5Y0KCKVKZeiTKm9Y+kV
| QbE/jTz0MsUw4Nvst84xQg/n2tSSISPKKHYOyrk0AIwf0AYwxVJ0uG6ELOkAgczV
| LKcZAz40yssIBG/CYCEIIwzvlrQx2JHUN54YHGyFyQTArZInSjWVAgMBAAGjJDAi
| MBMGA1UdJQQMMAoGCCsGAQUFBwMBMAsGA1UdDwQEAwIEMDANBgkqhkiG9w0BAQUF
| AAOCAQEAurf/kwXejlXRyz6Iw66txEyGkQuhccOWXP4hctsHKjxuPYkJGqYhJr1y
| cy4GoDz4tkCo4DDO4Neu2fg6loNi0o9BnLsFjimr2oUNP6WmO1dSBaYRjonf5tMd
| /LtWUIvZpXujY5NByrHtBnxn7y2Y4eKM99KrwQBtfIEii6LyrcS9q4H8+YWhavqB
| hOT8l2/X+J8WG3RrQGQSWvSlThonG63rg8C3hqi90UwPOsUcRGDrMndnVLe9xr0I
| vvqUA8qZILpqBVX3F+jzFfGwabQ4AV4EXbQqFkafH2+G7QYDXaY5MVNK2wpSt+uZ
| rsTMMfFNYpI89Z5OUdhabQoqGA8ARg==
|_-----END CERTIFICATE-----
5722/tcp  open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49154/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49155/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49157/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49158/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49165/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|phone|specialized
Running (JUST GUESSING): Microsoft Windows 2008|7|Vista|Phone|2012|8.1 (97%)
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_vista cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_8.1
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (97%), Microsoft Windows Server 2008 R2 or Windows 7 SP1 (92%), Microsoft Windows Vista or Windows 7 (92%), Microsoft Windows 8.1 Update 1 (92%), Microsoft Windows Phone 7.5 or 8.0 (92%), Microsoft Windows Server 2012 R2 (91%), Microsoft Windows Embedded Standard 7 (91%), Microsoft Windows Server 2008 R2 (89%), Microsoft Windows Server 2008 R2 or Windows 8.1 (89%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (89%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.95%E=4%D=9/2%OT=53%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=68B733F0%P=x86_64-pc-linux-gnu)
SEQ(SP=106%GCD=1%ISR=109%TI=I%II=I%SS=S%TS=7)
SEQ(SP=F9%GCD=1%ISR=106%TI=I%II=I%SS=S%TS=7)
OPS(O1=M552NW8ST11%O2=M552NW8ST11%O3=M552NW8NNT11%O4=M552NW8ST11%O5=M552NW8ST11%O6=M552ST11)
WIN(W1=2000%W2=2000%W3=2000%W4=2000%W5=2000%W6=2000)
ECN(R=Y%DF=Y%TG=80%W=2000%O=M552NW8NNS%CC=N%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=Y%DFI=N%TG=80%CD=Z)

Uptime guess: 0.008 days (since Tue Sep  2 23:33:12 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=249 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: Host: BLN01; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery:
|   OS: Windows Server 2008 R2 Datacenter 7601 Service Pack 1 (Windows Server 2008 R2 Datacenter 6.1)
|   OS CPE: cpe:/o:microsoft:windows_server_2008::sp1
|   Computer name: BLN01
|   NetBIOS computer name: BLN01\x00
|   Domain name: retro2.vl
|   Forest name: retro2.vl
|   FQDN: BLN01.retro2.vl
|_  System time: 2025-09-02T20:13:29+02:00
|_clock-skew: mean: -23m59s, deviation: 53m38s, median: 0s
| smb2-security-mode:
|   2:1:0:
|_    Message signing enabled and required
| p2p-conficker:
|   Checking for Conficker.C or higher...
|   Check 1 (port 25385/tcp): CLEAN (Timeout)
|   Check 2 (port 63732/tcp): CLEAN (Timeout)
|   Check 3 (port 8922/udp): CLEAN (Timeout)
|   Check 4 (port 46708/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-time:
|   date: 2025-09-02T18:13:30
|_  start_date: 2025-09-02T18:03:43

TRACEROUTE (using port 445/tcp)
HOP RTT      ADDRESS
1   68.53 ms 10.10.14.1
2   68.58 ms retrotwo.htb (10.129.67.220)

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:44
Completed NSE at 23:44, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:44
Completed NSE at 23:44, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:44
Completed NSE at 23:44, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 101.92 seconds
           Raw packets sent: 107 (8.392KB) | Rcvd: 58 (3.736KB)
```

### DNS (53)

```bash
53/tcp    open  domain        syn-ack ttl 127 Microsoft DNS 6.1.7601 (1DB15F75) (Windows Server 2008 R2 SP1)
| dns-nsid:
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15F75)
```

- Tried common enumeration - nothing too interesting
### SMB (135, 139, 445)

```bash
ashu@kali ~ smbclient -L \\\\retrotwo.htb\\
Password for [WORKGROUP\ashu]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        Public          Disk      
        SYSVOL          Disk      Logon server share 
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to retrotwo.htb failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

- Although we are able to list the shares, we cannot actually connect to and enumerate the shares.

```bash
smbclient \\\\retro2.vl\\Public   
Password for [WORKGROUP\ashu]:
Try "help" to get a list of possible commands.
smb: \> dir
  .                                   D        0  Sat Aug 17 20:00:37 2024
  ..                                  D        0  Sat Aug 17 20:00:37 2024
  DB                                  D        0  Sat Aug 17 17:37:06 2024
  Temp                                D        0  Sat Aug 17 17:28:05 2024

                6290943 blocks of size 4096. 803562 blocks available
smb: \> cd DB
smb: \DB\> dir
  .                                   D        0  Sat Aug 17 17:37:06 2024
  ..                                  D        0  Sat Aug 17 17:37:06 2024
  staff.accdb                         A   876544  Sat Aug 17 20:00:19 2024

                6290943 blocks of size 4096. 803562 blocks available
smb: \DB\> get staff.accdb 
getting file \DB\staff.accdb of size 876544 as staff.accdb (1105.9 KiloBytes/sec) (average 1105.9 KiloBytes/sec)
smb: \DB\> 

```

So, we got a `staff.accdb` 

Using `office2john` to get a hash of the password to get cracking the password.

```bash
ashu@kali ~ hashcat hash /usr/share/wordlists/rockyou.txt
$office$*2013*100000*256*16*5736cfcbb054e749a8f303570c5c1970*1ec683f4d8c4e9faf77d3c01f2433e56*7de0d4af8c54c33be322dbc860b68b4849f811196015a3f48a424a265d018235:class08
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 9600 (MS Office 2013)
Hash.Target......: $office$*2013*100000*256*16*5736cfcbb054e749a8f3035...018235
Time.Started.....: Wed Sep  3 00:42:37 2025 (8 secs)
Time.Estimated...: Wed Sep  3 00:42:45 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:      670 H/s (7.45ms) @ Accel:1024 Loops:512 Thr:1 Vec:4
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 5120/14344385 (0.04%)
Rejected.........: 0/5120 (0.00%)
Restore.Point....: 4096/14344385 (0.03%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: newzealand -> babygrl
Hardware.Mon.#1..: Util: 63%

Started: Wed Sep  3 00:42:17 2025
Stopped: Wed Sep  3 00:42:46 2025

```

We cracked the password and after opening this file we see this 

![[Pasted image 20250903005232.png]]

WE got a LDAP user and password.

```bash
ashu@kali ~ nxc smb retro2.vl -u 'ldapreader' -p 'ppYaVcB5R' --shares
SMB         10.129.67.220   445    BLN01            [*] Windows 7 / Server 2008 R2 Build 7601 x64 (name:BLN01) (domain:retro2.vl) (signing:True) (SMBv1:True) 
SMB         10.129.67.220   445    BLN01            [+] retro2.vl\ldapreader:ppYaVcB5R 
SMB         10.129.67.220   445    BLN01            [*] Enumerated shares
SMB         10.129.67.220   445    BLN01            Share           Permissions     Remark
SMB         10.129.67.220   445    BLN01            -----           -----------     ------
SMB         10.129.67.220   445    BLN01            ADMIN$                          Remote Admin
SMB         10.129.67.220   445    BLN01            C$                              Default share
SMB         10.129.67.220   445    BLN01            IPC$                            Remote IPC
SMB         10.129.67.220   445    BLN01            NETLOGON        READ            Logon server share 
SMB         10.129.67.220   445    BLN01            Public          READ            
SMB         10.129.67.220   445    BLN01            SYSVOL          READ            Logon server share 
```

### Bloodhound Enumeration

First, I tried to use the Bloodhound injestor build into netexec but it did not work.

Running bloodhound script of Tyler Ramsey we got some bloodhound loot.

```bash
ashu@kali ~ bash ad-bloodhound.sh                              
Domain: 
retro2.vl
Username: 
ldapreader
Password: 
ppYaVcB5R
IP of Domain: 
10.129.67.220
INFO: BloodHound.py for BloodHound LEGACY (BloodHound 4.2 and 4.3)
INFO: Found AD domain: retro2.vl
INFO: Getting TGT for user
INFO: Connecting to LDAP server: bln01.retro2.vl
INFO: Found 1 domains
INFO: Found 1 domains in the forest
INFO: Found 4 computers
INFO: Connecting to LDAP server: bln01.retro2.vl
INFO: Found 27 users
INFO: Found 43 groups
INFO: Found 2 gpos
INFO: Found 2 ous
INFO: Found 19 containers
INFO: Found 0 trusts
INFO: Starting computer enumeration with 10 workers
INFO: Querying computer: 
INFO: Querying computer: 
INFO: Querying computer: 
INFO: Querying computer: BLN01.retro2.vl
INFO: Done in 00M 16S

```

```bash
ashu@kali ~ ls Bloodhound_Loot 
 20250903010635_computers.json    20250903010635_domains.json   20250903010635_groups.json   20250903010635_users.json
 20250903010635_containers.json   20250903010635_gpos.json      20250903010635_ous.json

```