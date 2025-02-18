### Silver Platter Machine

[https://tryhackme.com/room/silverplatter](https://tryhackme.com/room/silverplatter)


1. Pinging the target

```bash

ashu㉿kali ~/TryHackMe/SilverPlatter $ ping silverplatter.thm
PING silverplatter.thm (10.10.223.110) 56(84) bytes of data.
64 bytes from silverplatter.thm (10.10.223.110): icmp_seq=1 ttl=60 time=285 ms
64 bytes from silverplatter.thm (10.10.223.110): icmp_seq=2 ttl=60 time=244 ms
64 bytes from silverplatter.thm (10.10.223.110): icmp_seq=3 ttl=60 time=207 ms
^C
--- silverplatter.thm ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 207.271/245.229/284.809/31.675 ms

```

2. Scanning The Target

```bash
ashu ㉿kali  ~  sudo rustscan -a silverplatter.thm -- -A                                                                                                                                                                                              
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.                                                                                                                                                                                                     
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |                                                                                                                                                                                                     
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |                                                                                                                                                                                                     
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'                                                                                                                                                                                                     
The Modern Day Port Scanner.                                                                                                                                                                                                                                 
________________________________________                                                                                                                                                                                                                     
: http://discord.skerritt.blog         :                                                                                                                                                                                                                     
: https://github.com/RustScan/RustScan :                                                                                                                                                                                                                     
 --------------------------------------                                                                                                                                                                                                                      
TCP handshake? More like a friendly high-five!                                                                                                                                                                                                               
                                                                                                                                                                                                                                                             
[~] The config file is expected to be at "/root/.rustscan.toml"                                                                                                                                                                                              
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers                                                                                                                                          
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.                                                                                                                   
Open 10.10.223.110:22                                                                                                                                                                                                                                        
Open 10.10.223.110:80                                                                                                                                                                                                                                        
[~] Starting Script(s)                                                                                                                                                                                                                                       
[>] Running script "nmap -vvv -p {{port}} {{ip}} -A" on ip 10.10.223.110                                                                                                                                                                                     
Depending on the complexity of the script, results may take some time to appear.                                                                                                                                                                             
[~] Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-18 12:26 EST                                                                                                                                                                                          
NSE: Loaded 157 scripts for scanning.                                                                                                                                                                                                                        
NSE: Script Pre-scanning.                                                                                                                                                                                                                                    
NSE: Starting runlevel 1 (of 3) scan.                                                                                                                                                                                                                        
Initiating NSE at 12:26                                                                                                                                                                                                                                      
Completed NSE at 12:26, 0.00s elapsed                                                                                                                                                                                                                        
NSE: Starting runlevel 2 (of 3) scan.                                                                                                                                                                                                                        
Initiating NSE at 12:26                                                                                                                                                                                                                                      
Completed NSE at 12:26, 0.00s elapsed                                                                                                                                                                                                                        
NSE: Starting runlevel 3 (of 3) scan.                                                                                                                                                                                                                        
Initiating NSE at 12:26                                                                                                                                                                                                                                      
Completed NSE at 12:26, 0.00s elapsed                                                                                                                                                                                                                        
Initiating Ping Scan at 12:26                                                                                                                                                                                                                                
Scanning 10.10.223.110 [4 ports]                                                                                                                                                                                                                             
Completed Ping Scan at 12:26, 0.20s elapsed (1 total hosts)                                                                                                                                                                                                  
Initiating SYN Stealth Scan at 12:26                                                                                                                                                                                                                         
Scanning silverplatter.thm (10.10.223.110) [2 ports]                                                                                                                                                                                                         
Discovered open port 22/tcp on 10.10.223.110                                                                                                                                                                                                                 
Discovered open port 80/tcp on 10.10.223.110                                                                                                                                                                                                                 
Completed SYN Stealth Scan at 12:26, 0.20s elapsed (2 total ports)                                                                                                                                                                                           
Initiating Service scan at 12:26                                                                                                                                                                                                                             
Scanning 2 services on silverplatter.thm (10.10.223.110)                                                                                                                                                                                                     
Completed Service scan at 12:26, 11.85s elapsed (2 services on 1 host)                                                                                                                                                                                       
Initiating OS detection (try #1) against silverplatter.thm (10.10.223.110)                                                                                                                                                                                   
Initiating Traceroute at 12:26                                                                                                                                                                                                                               
Completed Traceroute at 12:26, 3.02s elapsed                                                                                                                                                                                                                 
Initiating Parallel DNS resolution of 1 host. at 12:26                                                                                                                                                                                                       
Completed Parallel DNS resolution of 1 host. at 12:26, 0.05s elapsed                                                                                                                                                                                         
DNS resolution of 1 IPs took 0.05s. Mode: Async [#: 3, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]                                                                                                                                                             
NSE: Script scanning 10.10.223.110.                            
NSE: Starting runlevel 1 (of 3) scan.                          
Initiating NSE at 12:26                                        
Completed NSE at 12:26, 25.32s elapsed                         
NSE: Starting runlevel 2 (of 3) scan.                          
Initiating NSE at 12:26                                        
Completed NSE at 12:26, 7.79s elapsed                          
NSE: Starting runlevel 3 (of 3) scan.                          
Initiating NSE at 12:26                                        
Completed NSE at 12:26, 0.00s elapsed                          
Nmap scan report for silverplatter.thm (10.10.223.110)                                                                        
Host is up, received reset ttl 60 (0.18s latency).                                                                            
Scanned at 2025-02-18 12:26:06 EST for 51s           
```



### Rustscan Syntax

This too does what above nmap scan does 
```bash
rustscan -a [Target IP] -- -A

-a - Tells this is the target scan for open ports
-- - this passes the output to nmap and tells nmap to run a full version detection scan which is followed by the -A switch just like we specified in the above nmap command
```



### Conclusion 

We found 3 Open ports
1. 22 SSH
2. 80 HTTP Server
3. 8080 Another Webserver Running