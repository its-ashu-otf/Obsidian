---
aliases:
  - "Assessment Methodologies: Footprinting and Scanning CTF 1"
---
# Overview

Reconnaissance is the initial phase of a penetration testing process where information about a target system is gathered to identify potential vulnerabilities. This phase involves actively or passively collecting data such as server headers, open ports, exposed directories, and system configurations. Techniques like scanning, querying DNS records, examining web application files (e.g., robots.txt), and analyzing response headers help uncover critical information that can aid in later exploitation phases. Effective reconnaissance allows testers to map the attack surface, prioritize targets, and plan their approach with minimal detection by the system's defenses.

This lab is designed to test your knowledge and skills in performing reconnaissance and identifying hidden information on a target web server.

# Lab Environment

In this lab environment, you will be provided with GUI access to a Kali Linux machine. The target machine will be accessible at **http://target.ine.local**.

**Objective:** Perform reconnaissance on the target and capture all the flags hidden within the environment.

**Flags to Capture:**

- **Flag 1**: The server proudly announces its identity in every response. Look closely; you might find something unusual.
- **Flag 2**: The gatekeeper's instructions often reveal what should remain unseen. Don't forget to read between the lines.
- **Flag 3**: Anonymous access sometimes leads to forgotten treasures. Connect and explore the directory; you might stumble upon something valuable.
- **Flag 4**: A well-named database can be quite revealing. Peek at the configurations to discover the hidden treasure.

# Tools

The best tools for this lab are:

- Nmap
- FTP
- MySQL

---

### Note

In this lab, the flag will follow the format: FLAG1_MD5Hash. For example, FLAG1_0f4d0db3668dd58cabb9eb409657eaa8. You need to submit only the MD5 hash string, excluding the underscore (_). For instance: 0f4d0db3668dd58cabb9eb409657eaa8.


# Walkthrough

##  **Flag 1**: The server proudly announces its identity in every response. Look closely; you might find something unusual.

```bash
┌──(root㉿INE)-[~]
└─# nmap -sS -sC -sV -p- -T4 target.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-04-27 23:47 IST
Nmap scan report for target.ine.local (192.122.91.3)
Host is up (0.000026s latency).
Not shown: 65527 closed tcp ports (reset)
PORT      STATE SERVICE  VERSION
21/tcp    open  ftp      vsftpd 3.0.5
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 0        0              22 Oct 28 06:11 creds.txt
|_-rw-r--r--    1 0        0              39 Apr 27 18:09 flag.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.122.91.2
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.5 - secure, fast, stable
|_End of status
22/tcp    open  ssh      OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 a5:93:0f:6b:5a:77:f1:77:e8:2e:c9:31:e7:df:66:06 (ECDSA)
|_  256 b6:0d:e4:92:36:30:79:b7:31:91:3b:a0:1f:c1:ee:85 (ED25519)
25/tcp    open  smtp     Postfix smtpd
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost
| Not valid before: 2024-10-28T06:10:50
|_Not valid after:  2034-10-26T06:10:50
|_smtp-commands: localhost.members.linode.com, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING
80/tcp    open  http     Werkzeug/3.0.6 Python/3.10.12
| http-robots.txt: 3 disallowed entries 
|_/photos /secret-info/ /data/
|_http-server-header: Werkzeug/3.0.6 Python/3.10.12
|_http-title: CTF Challenge
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/3.0.6 Python/3.10.12
|     Date: Sun, 27 Apr 2025 18:17:25 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 2557
|     Server: FLAG1_e82d7cc61e1b4401b9222b76c21d02c2
|     Connection: close
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="UTF-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <link rel="shortcut icon" href="#">
|     <title>CTF Challenge</title>
|     <style>
|     body {
|     font-family: 'Arial', sans-serif;
|     margin: 0;
|     padding: 0;
|     background-color: #1c1c1c;
|     color: #fff;
|     background-color: #333;
|     padding: 15px;
|     text-align: center;
|     list-style: none;
|     margin: 0;
|     padding: 0;
|     display:
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/3.0.6 Python/3.10.12
|     Date: Sun, 27 Apr 2025 18:17:25 GMT
|     Content-Type: text/html; charset=utf-8
|     Allow: OPTIONS, HEAD, GET
|     Server: FLAG1_e82d7cc61e1b4401b9222b76c21d02c2
|     Content-Length: 0
|_    Connection: close
143/tcp   open  imap     Dovecot imapd (Ubuntu)
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: IMAP4rev1 SASL-IR more have LOGIN-REFERRALS capabilities listed IDLE Pre-login post-login OK LOGINDISABLEDA0001 LITERAL+ ID ENABLE STARTTLS
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost
| Not valid before: 2024-10-28T06:10:50
|_Not valid after:  2034-10-26T06:10:50
993/tcp   open  ssl/imap Dovecot imapd (Ubuntu)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost
| Not valid before: 2024-10-28T06:10:50
|_Not valid after:  2034-10-26T06:10:50
|_imap-capabilities: IMAP4rev1 SASL-IR more LOGIN-REFERRALS have listed IDLE Pre-login post-login capabilities OK LITERAL+ ID ENABLE AUTH=PLAINA0001
3306/tcp  open  mysql    MySQL 8.0.39-0ubuntu0.22.04.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=MySQL_Server_8.0.39_Auto_Generated_Server_Certificate
| Not valid before: 2024-10-28T06:11:13
|_Not valid after:  2034-10-26T06:11:13
| mysql-info: 
|   Protocol: 10
|   Version: 8.0.39-0ubuntu0.22.04.1
|   Thread ID: 116
|   Capabilities flags: 65535
|   Some Capabilities: Support41Auth, ODBCClient, SupportsTransactions, DontAllowDatabaseTableColumn, LongPassword, IgnoreSpaceBeforeParenthesis, InteractiveClient, Speaks41ProtocolNew, FoundRows, SupportsCompression, SwitchToSSLAfterHandshake, Speaks41ProtocolOld, SupportsLoadDataLocal, IgnoreSigpipes, LongColumnFlag, ConnectWithDatabase, SupportsAuthPlugins, SupportsMultipleStatments, SupportsMultipleResults
|   Status: Autocommit
|   Salt: ol`\x13j\x157\x0C.)'P6Zgvu\x11%
|_  Auth Plugin Name: caching_sha2_password
33060/tcp open  mysqlx?
| fingerprint-strings: 
|   DNSStatusRequestTCP, LDAPSearchReq, NotesRPC, SSLSessionReq, TLSSessionReq, X11Probe, afp: 
|     Invalid message"
|     HY000
|   LDAPBindReq: 
|     *Parse error unserializing protobuf message"
|     HY000
|   oracle-tns: 
|     Invalid message-frame."
|_    HY000
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port80-TCP:V=7.94SVN%I=7%D=4/27%Time=680E74B5%P=x86_64-pc-linux-gnu%r(G
SF:etRequest,ADD,"HTTP/1\.1\x20200\x20OK\r\nServer:\x20Werkzeug/3\.0\.6\x2
SF:0Python/3\.10\.12\r\nDate:\x20Sun,\x2027\x20Apr\x202025\x2018:17:25\x20
SF:GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\
SF:x202557\r\nServer:\x20FLAG1_e82d7cc61e1b4401b9222b76c21d02c2\r\nConnect
SF:ion:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en\">\n<head>\
SF:n\x20\x20\x20\x20<meta\x20charset=\"UTF-8\">\n\x20\x20\x20\x20<meta\x20
SF:name=\"viewport\"\x20content=\"width=device-width,\x20initial-scale=1\.
SF:0\">\n\x20\x20\x20\x20<link\x20rel=\"shortcut\x20icon\"\x20href=\"#\">\
SF:n\x20\x20\x20\x20<title>CTF\x20Challenge</title>\n\x20\x20\x20\x20<styl
SF:e>\n\x20\x20\x20\x20\x20\x20\x20\x20body\x20{\n\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20font-family:\x20'Arial',\x20sans-serif;\n\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20margin:\x200;\n\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20padding:\x200;\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20background-color:\x20#1c1c1c;\n\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20color:\x20#fff;\n\x20\x20\x20\x20\x2
SF:0\x20\x20\x20}\n\n\x20\x20\x20\x20\x20\x20\x20\x20nav\x20{\n\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20background-color:\x20#333;\n\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20padding:\x2015px;\n\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20text-align:\x20center;\n\x20\x20\
SF:x20\x20\x20\x20\x20\x20}\n\n\x20\x20\x20\x20\x20\x20\x20\x20nav\x20ul\x
SF:20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20list-style:\x20non
SF:e;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20margin:\x200;\n\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20padding:\x200;\n\x20\x20\x2
SF:0\x20\x20\x20\x20\x20}\n\n\x20\x20\x20\x20\x20\x20\x20\x20nav\x20ul\x20
SF:li\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20display:\x20")
SF:%r(HTTPOptions,F8,"HTTP/1\.1\x20200\x20OK\r\nServer:\x20Werkzeug/3\.0\.
SF:6\x20Python/3\.10\.12\r\nDate:\x20Sun,\x2027\x20Apr\x202025\x2018:17:25
SF:\x20GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nAllow:\x20OP
SF:TIONS,\x20HEAD,\x20GET\r\nServer:\x20FLAG1_e82d7cc61e1b4401b9222b76c21d
SF:02c2\r\nContent-Length:\x200\r\nConnection:\x20close\r\n\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port33060-TCP:V=7.94SVN%I=7%D=4/27%Time=680E74B5%P=x86_64-pc-linux-gnu%
SF:r(NULL,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(GenericLines,9,"\x05\0\0\0\x
SF:0b\x08\x05\x1a\0")%r(GetRequest,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(HTT
SF:POptions,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(RTSPRequest,9,"\x05\0\0\0\
SF:x0b\x08\x05\x1a\0")%r(RPCCheck,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(DNSV
SF:ersionBindReqTCP,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(DNSStatusRequestTC
SF:P,2B,"\x05\0\0\0\x0b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x
SF:0fInvalid\x20message\"\x05HY000")%r(Help,9,"\x05\0\0\0\x0b\x08\x05\x1a\
SF:0")%r(SSLSessionReq,2B,"\x05\0\0\0\x0b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\
SF:x01\x10\x88'\x1a\x0fInvalid\x20message\"\x05HY000")%r(TerminalServerCoo
SF:kie,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(TLSSessionReq,2B,"\x05\0\0\0\x0
SF:b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20messag
SF:e\"\x05HY000")%r(Kerberos,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(SMBProgNe
SF:g,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(X11Probe,2B,"\x05\0\0\0\x0b\x08\x
SF:05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message\"\x05
SF:HY000")%r(FourOhFourRequest,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(LPDStri
SF:ng,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(LDAPSearchReq,2B,"\x05\0\0\0\x0b
SF:\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1a\x0fInvalid\x20message
SF:\"\x05HY000")%r(LDAPBindReq,46,"\x05\0\0\0\x0b\x08\x05\x1a\x009\0\0\0\x
SF:01\x08\x01\x10\x88'\x1a\*Parse\x20error\x20unserializing\x20protobuf\x2
SF:0message\"\x05HY000")%r(SIPOptions,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(
SF:LANDesk-RC,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(TerminalServer,9,"\x05\0
SF:\0\0\x0b\x08\x05\x1a\0")%r(NCP,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(Note
SF:sRPC,2B,"\x05\0\0\0\x0b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\x10\x88'\x1
SF:a\x0fInvalid\x20message\"\x05HY000")%r(JavaRMI,9,"\x05\0\0\0\x0b\x08\x0
SF:5\x1a\0")%r(WMSRequest,9,"\x05\0\0\0\x0b\x08\x05\x1a\0")%r(oracle-tns,3
SF:2,"\x05\0\0\0\x0b\x08\x05\x1a\0%\0\0\0\x01\x08\x01\x10\x88'\x1a\x16Inva
SF:lid\x20message-frame\.\"\x05HY000")%r(ms-sql-s,9,"\x05\0\0\0\x0b\x08\x0
SF:5\x1a\0")%r(afp,2B,"\x05\0\0\0\x0b\x08\x05\x1a\0\x1e\0\0\0\x01\x08\x01\
SF:x10\x88'\x1a\x0fInvalid\x20message\"\x05HY000");
MAC Address: 02:42:C0:7A:5B:03 (Unknown)
Service Info: Host:  localhost.members.linode.com; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 91.90 seconds

```


```bash
HTTPOptions: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/3.0.6 Python/3.10.12
|     Date: Sun, 27 Apr 2025 18:17:25 GMT
|     Content-Type: text/html; charset=utf-8
|     Allow: OPTIONS, HEAD, GET
|     Server: FLAG1_e82d7cc61e1b4401b9222b76c21d02c2
|     Content-Length: 0
|_    Connection: close
```

### Another way of getting the flag

```bash

┌──(root㉿INE)-[~]
└─# curl --head target.ine.local
HTTP/1.1 200 OK
Server: Werkzeug/3.0.6 Python/3.10.12
Date: Sun, 27 Apr 2025 18:27:49 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 2557
Server: FLAG1_e82d7cc61e1b4401b9222b76c21d02c2
Connection: close


```

Got the first flag.

##  **Flag 2**: The gatekeeper's instructions often reveal what should remain unseen. Don't forget to read between the lines.

So, this one was tricky but I still got around it 

The target is also a webserver. So navigating to the website I got this

![[Pasted image 20250428000102.png]]

So, I tried to check for `robots.txt` and got something of interest 

![[Pasted image 20250428000210.png]]

So, here is something related to `/secret-info`

Let's access the directory 

![[Pasted image 20250428000251.png]]

Upon accessing it it holds the flag, Let's access it

![[Pasted image 20250428000325.png]]

Got the 2nd flag too.
## **Flag 3**: Anonymous access sometimes leads to forgotten treasures. Connect and explore the directory; you might stumble upon something valuable.

1. Let's check if anonymous login is allowed or not using nmap scripting engine

```bash
┌──(root㉿INE)-[~]
└─# nmap -sS target.ine.local --script=ftp-anon.nse
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-04-27 23:50 IST
Nmap scan report for target.ine.local (192.122.91.3)
Host is up (0.000026s latency).
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 0        0              22 Oct 28 06:11 creds.txt
|_-rw-r--r--    1 0        0              39 Apr 27 18:09 flag.txt
22/tcp   open  ssh
25/tcp   open  smtp
80/tcp   open  http
143/tcp  open  imap
993/tcp  open  imaps
3306/tcp open  mysql
MAC Address: 02:42:C0:7A:5B:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.24 seconds

```

2. So, it is let's login using `anonymous` for username and same for the password

```bash

┌──(root㉿INE)-[~]
└─# ftp target.ine.local
Connected to target.ine.local.
220 (vsFTPd 3.0.5)
Name (target.ine.local:root): anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||58905|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              22 Oct 28 06:11 creds.txt
-rw-r--r--    1 0        0              39 Apr 27 18:09 flag.txt
226 Directory send OK.
ftp> get creds.txt
local: creds.txt remote: creds.txt
229 Entering Extended Passive Mode (|||49928|)
150 Opening BINARY mode data connection for creds.txt (22 bytes).
100% |**********************************************************************************************************************************************************************************************|    22      173.26 KiB/s    00:00 ETA
226 Transfer complete.
22 bytes received in 00:00 (39.27 KiB/s)
ftp> get flag.txt
local: flag.txt remote: flag.txt
229 Entering Extended Passive Mode (|||10681|)
150 Opening BINARY mode data connection for flag.txt (39 bytes).
100% |**********************************************************************************************************************************************************************************************|    39      865.58 KiB/s    00:00 ETA
226 Transfer complete.
39 bytes received in 00:00 (123.25 KiB/s)
ftp> 
ftp> 


```

```bash
┌──(root㉿INE)-[~]
└─# cat flag.txt 
FLAG3_62da729a9afe424e8a2026138a04e40f

```

Got the 3rd Flag

## **Flag 4**: A well-named database can be quite revealing. Peek at the configurations to discover the hidden treasure.

In the above 3rd flag I got a `creds.txt`  which holds following information

```bash 

┌──(root㉿INE)-[~]
└─# cat creds.txt 
db_admin:password@123
```

I think this is the password to connect to the MySQL database

Let's connect

  ```bash
  
┌──(root㉿INE)-[~]
└─# mysql -h target.ine.local -u db_admin -p              
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 128
Server version: 8.0.39-0ubuntu0.22.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Support MariaDB developers by giving a star at https://github.com/MariaDB/server
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]> show databases
    -> 
    -> ^C
MySQL [(none)]> show databases;
+----------------------------------------+
| Database                               |
+----------------------------------------+
| FLAG4_9d48e061c48e4a2ab31c25b46e29d00d |
| information_schema                     |
| mysql                                  |
| performance_schema                     |
| sys                                    |
+----------------------------------------+
5 rows in set (0.002 sec)

MySQL [(none)]> 

```

Got the 4th final flag. 
