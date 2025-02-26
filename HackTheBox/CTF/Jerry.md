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

here, I hit the /revshell 
