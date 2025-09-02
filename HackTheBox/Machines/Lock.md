## Enumeration

### NMAP Scan

```bash
# Nmap 7.95 scan initiated Tue Sep  2 21:36:03 2025 as: /usr/lib/nmap/nmap -A -T4 -oN lock_nmap_scan.txt lock.htb
Nmap scan report for lock.vl (10.129.234.64)
Host is up (0.056s latency).
Not shown: 996 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-title: Lock - Index
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
445/tcp  open  microsoft-ds?
3000/tcp open  http          Golang net/http server
|_http-title: Gitea: Git with a cup of tea
| fingerprint-strings: 
|   GenericLines, Help, RTSPRequest: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Cache-Control: max-age=0, private, must-revalidate, no-transform
|     Content-Type: text/html; charset=utf-8
|     Set-Cookie: i_like_gitea=cd4c570f5b8a87e1; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=rumexpdk0ZYE5tbMU9Sesgkj14E6MTc1NjgyOTE3NTIxMTc2OTUwMA; Path=/; Max-Age=86400; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 02 Sep 2025 16:06:15 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-auto">
|     <head>
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <title>Gitea: Git with a cup of tea</title>
|     <link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSIsInNob3J0X25hbWUiOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdXJsIjoiaHR0cDovL2xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi8vbG9jYWxob3N0OjMwMDAvYXNzZXRzL2ltZy9sb2dvLnBuZyIsInR5cGUiOiJpbWFnZS9wbmciLCJzaXplcyI6IjU
|   HTTPOptions: 
|     HTTP/1.0 405 Method Not Allowed
|     Allow: HEAD
|     Allow: GET
|     Cache-Control: max-age=0, private, must-revalidate, no-transform
|     Set-Cookie: i_like_gitea=5ee3c797f5de0452; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=1MQvC4NGCQgKwmTYQHqBvf_FDlw6MTc1NjgyOTE3NTQ1OTgzOTMwMA; Path=/; Max-Age=86400; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 02 Sep 2025 16:06:15 GMT
|_    Content-Length: 0
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2025-09-02T16:07:21+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=Lock
| Not valid before: 2025-04-15T00:34:47
|_Not valid after:  2025-10-15T00:34:47
| rdp-ntlm-info: 
|   Target_Name: LOCK
|   NetBIOS_Domain_Name: LOCK
|   NetBIOS_Computer_Name: LOCK
|   DNS_Domain_Name: Lock
|   DNS_Computer_Name: Lock
|   Product_Version: 10.0.20348
|_  System_Time: 2025-09-02T16:06:41+00:00
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3000-TCP:V=7.95%I=7%D=9/2%Time=68B715F6%P=x86_64-pc-linux-gnu%r(Gen
SF:ericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20te
SF:xt/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x2
SF:0Request")%r(GetRequest,3000,"HTTP/1\.0\x20200\x20OK\r\nCache-Control:\
SF:x20max-age=0,\x20private,\x20must-revalidate,\x20no-transform\r\nConten
SF:t-Type:\x20text/html;\x20charset=utf-8\r\nSet-Cookie:\x20i_like_gitea=c
SF:d4c570f5b8a87e1;\x20Path=/;\x20HttpOnly;\x20SameSite=Lax\r\nSet-Cookie:
SF:\x20_csrf=rumexpdk0ZYE5tbMU9Sesgkj14E6MTc1NjgyOTE3NTIxMTc2OTUwMA;\x20Pa
SF:th=/;\x20Max-Age=86400;\x20HttpOnly;\x20SameSite=Lax\r\nX-Frame-Options
SF::\x20SAMEORIGIN\r\nDate:\x20Tue,\x2002\x20Sep\x202025\x2016:06:15\x20GM
SF:T\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en-US\"\x20class=\"theme-a
SF:uto\">\n<head>\n\t<meta\x20name=\"viewport\"\x20content=\"width=device-
SF:width,\x20initial-scale=1\">\n\t<title>Gitea:\x20Git\x20with\x20a\x20cu
SF:p\x20of\x20tea</title>\n\t<link\x20rel=\"manifest\"\x20href=\"data:appl
SF:ication/json;base64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSI
SF:sInNob3J0X25hbWUiOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdX
SF:JsIjoiaHR0cDovL2xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi8vb
SF:G9jYWxob3N0OjMwMDAvYXNzZXRzL2ltZy9sb2dvLnBuZyIsInR5cGUiOiJpbWFnZS9wbmci
SF:LCJzaXplcyI6IjU")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nCont
SF:ent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r
SF:\n400\x20Bad\x20Request")%r(HTTPOptions,197,"HTTP/1\.0\x20405\x20Method
SF:\x20Not\x20Allowed\r\nAllow:\x20HEAD\r\nAllow:\x20GET\r\nCache-Control:
SF:\x20max-age=0,\x20private,\x20must-revalidate,\x20no-transform\r\nSet-C
SF:ookie:\x20i_like_gitea=5ee3c797f5de0452;\x20Path=/;\x20HttpOnly;\x20Sam
SF:eSite=Lax\r\nSet-Cookie:\x20_csrf=1MQvC4NGCQgKwmTYQHqBvf_FDlw6MTc1NjgyO
SF:TE3NTQ1OTgzOTMwMA;\x20Path=/;\x20Max-Age=86400;\x20HttpOnly;\x20SameSit
SF:e=Lax\r\nX-Frame-Options:\x20SAMEORIGIN\r\nDate:\x20Tue,\x2002\x20Sep\x
SF:202025\x2016:06:15\x20GMT\r\nContent-Length:\x200\r\n\r\n")%r(RTSPReque
SF:st,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plai
SF:n;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Reques
SF:t");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2022|2012|2016 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2022 cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_server_2016
Aggressive OS guesses: Microsoft Windows Server 2022 (89%), Microsoft Windows Server 2012 R2 (85%), Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-09-02T16:06:43
|_  start_date: N/A

TRACEROUTE (using port 445/tcp)
HOP RTT      ADDRESS
1   53.07 ms 10.10.14.1
2   55.65 ms lock.htb (10.129.234.64)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Sep  2 21:37:21 2025 -- 1 IP address (1 host up) scanned in 77.71 seconds

```

### Rustscan

```bash
 rustscan -a lock.vl -- -A -O lock_rustscan.txt
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
0day was here ♥

[~] The config file is expected to be at "/home/ashu/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.
Open 10.129.234.64:80
Open 10.129.234.64:445
Open 10.129.234.64:3000
Open 10.129.234.64:3389
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -A -O lock_rustscan.txt" on ip 10.129.234.64
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-02 21:46 IST
NSE: Loaded 157 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 21:46
Completed NSE at 21:46, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 21:46
Completed NSE at 21:46, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 21:46
Completed NSE at 21:46, 0.00s elapsed
Initiating Ping Scan at 21:46
Scanning 10.129.234.64 [4 ports]
Completed Ping Scan at 21:46, 0.10s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 21:46
Scanning lock.vl (10.129.234.64) [4 ports]
Discovered open port 80/tcp on 10.129.234.64
Discovered open port 3389/tcp on 10.129.234.64
Discovered open port 445/tcp on 10.129.234.64
Discovered open port 3000/tcp on 10.129.234.64
Completed SYN Stealth Scan at 21:46, 0.07s elapsed (4 total ports)
Initiating Service scan at 21:46
Scanning 4 services on lock.vl (10.129.234.64)
Completed Service scan at 21:46, 27.54s elapsed (4 services on 1 host)
Initiating OS detection (try #1) against lock.vl (10.129.234.64)
Retrying OS detection (try #2) against lock.vl (10.129.234.64)
Initiating Traceroute at 21:46
Completed Traceroute at 21:46, 0.07s elapsed
Initiating Parallel DNS resolution of 1 host. at 21:46
Completed Parallel DNS resolution of 1 host. at 21:46, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
NSE: Script scanning 10.129.234.64.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 21:46
NSE Timing: About 99.82% done; ETC: 21:47 (0:00:00 remaining)
Completed NSE at 21:47, 40.04s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 21:47
Completed NSE at 21:47, 0.28s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 21:47
Completed NSE at 21:47, 0.00s elapsed
Nmap scan report for lock.vl (10.129.234.64)
Host is up, received echo-reply ttl 127 (0.055s latency).
Scanned at 2025-09-02 21:46:24 IST for 73s

PORT     STATE SERVICE       REASON          VERSION
80/tcp   open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-title: Lock - Index
|_http-favicon: Unknown favicon MD5: FED84E16B6CCFE88EE7FFAAE5DFEFD34
| http-methods:
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
445/tcp  open  microsoft-ds? syn-ack ttl 127
3000/tcp open  http          syn-ack ttl 127 Golang net/http server
|_http-title: Gitea: Git with a cup of tea
|_http-favicon: Unknown favicon MD5: F6E1A9128148EEAD9EFF823C540EF471
| fingerprint-strings:
|   GenericLines, Help, RTSPRequest:
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest:
|     HTTP/1.0 200 OK
|     Cache-Control: max-age=0, private, must-revalidate, no-transform
|     Content-Type: text/html; charset=utf-8
|     Set-Cookie: i_like_gitea=21c82aaaa9ae2077; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=4O_jVgDrUJdc4Q-33OWhmDwmmPo6MTc1NjgyOTc5MTAwMjgyNDQwMA; Path=/; Max-Age=86400; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 02 Sep 2025 16:16:31 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-auto">
|     <head>
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <title>Gitea: Git with a cup of tea</title>
|     <link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSIsInNob3J0X25hbWUiOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdXJsIjoiaHR0cDovL2xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi8vbG9jYWxob3N0OjMwMDAvYXNzZXRzL2ltZy9sb2dvLnBuZyIsInR5cGUiOiJpbWFnZS9wbmciLCJzaXplcyI6IjU
|   HTTPOptions:
|     HTTP/1.0 405 Method Not Allowed
|     Allow: HEAD
|     Allow: GET
|     Cache-Control: max-age=0, private, must-revalidate, no-transform
|     Set-Cookie: i_like_gitea=21ebc1d17db0bf97; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=uAInThDzfWInhQq0IXC0SK1C3HM6MTc1NjgyOTc5MTI1OTUwMTYwMA; Path=/; Max-Age=86400; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 02 Sep 2025 16:16:31 GMT
|_    Content-Length: 0
| http-methods:
|_  Supported Methods: HEAD GET
3389/tcp open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: LOCK
|   NetBIOS_Domain_Name: LOCK
|   NetBIOS_Computer_Name: LOCK
|   DNS_Domain_Name: Lock
|   DNS_Computer_Name: Lock
|   Product_Version: 10.0.20348
|_  System_Time: 2025-09-02T16:16:57+00:00
| ssl-cert: Subject: commonName=Lock
| Issuer: commonName=Lock
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-04-15T00:34:47
| Not valid after:  2025-10-15T00:34:47
| MD5:   a26b:6f48:753d:e8cf:55e6:dc59:f8db:a2a9
| SHA-1: 1f19:4a17:9f9f:ca14:3202:9866:2228:b734:bbaa:e3ed
| -----BEGIN CERTIFICATE-----
| MIICzDCCAbSgAwIBAgIQUlCHKOG7FIJNwgrS/hCYJDANBgkqhkiG9w0BAQsFADAP
| MQ0wCwYDVQQDEwRMb2NrMB4XDTI1MDQxNTAwMzQ0N1oXDTI1MTAxNTAwMzQ0N1ow
| DzENMAsGA1UEAxMETG9jazCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
| ALLCn29jyiwHEpc5y/E359aMyxMW+fXgpEjwVFEHNufsK7v1riTHlN0M2IVhKc8K
| BYzSVy9nRXxj1eB+6vHAuWbMCwU2E9AiSCU1k1HmqZzThXg5oSpFQh7vCvCEcuzr
| ZETW/HBw5r/BxY1MF3jKzZoQzEFK6FljAkS5jeaI+sXHeE1ZgM+hh8jyb2Q7bA3F
| LIvZauR6h9mRKHdsqbc1DgbALzaGsOhhtT2wptocttz/C7z4sD9F3IsjUJWNr+Ci
| Quibs158YsQrbDfWlsIfsRLL0CDL/MZUHq+uaI0fu0zxEdg0Sirux3s0TDx8Nbep
| wJUJwsQ2IuXFyNOkJS5fU3UCAwEAAaMkMCIwEwYDVR0lBAwwCgYIKwYBBQUHAwEw
| CwYDVR0PBAQDAgQwMA0GCSqGSIb3DQEBCwUAA4IBAQCCJslalu1Xv+sHAz8pzKMg
| +v8qWECe9YsMXgiY80094GjKNlwPrfA2jOrxdDQXOB+B2897XQIHM2IKIo9kybZO
| BlIo40a0Yd+LW2LhbvDzBZoh4K+XjqtOUgn07gOMQEK0CqUFFjPVe8px5XmBft25
| 0KgsJ5/EyocarfZiZn0LbIwGvxR2q2rOhry5sRJoGdNqFDiVfQa5etbChibSM/rh
| VfjowpwylnASWruZo6HXrfsPgBgJmbFakPR88DkbH4MbSYUkyCTTSdLLybrWqKMe
| IHicwjmXiNlNWdmi5BmfQEq0Lh9qIrq093ITZghq6Ne2U18d0HndpEeAo/aogkWU
|_-----END CERTIFICATE-----
|_ssl-date: 2025-09-02T16:17:37+00:00; +1s from scanner time.
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3000-TCP:V=7.95%I=7%D=9/2%Time=68B7185E%P=x86_64-pc-linux-gnu%r(Gen
SF:ericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20te
SF:xt/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x2
SF:0Request")%r(GetRequest,3000,"HTTP/1\.0\x20200\x20OK\r\nCache-Control:\
SF:x20max-age=0,\x20private,\x20must-revalidate,\x20no-transform\r\nConten
SF:t-Type:\x20text/html;\x20charset=utf-8\r\nSet-Cookie:\x20i_like_gitea=2
SF:1c82aaaa9ae2077;\x20Path=/;\x20HttpOnly;\x20SameSite=Lax\r\nSet-Cookie:
SF:\x20_csrf=4O_jVgDrUJdc4Q-33OWhmDwmmPo6MTc1NjgyOTc5MTAwMjgyNDQwMA;\x20Pa
SF:th=/;\x20Max-Age=86400;\x20HttpOnly;\x20SameSite=Lax\r\nX-Frame-Options
SF::\x20SAMEORIGIN\r\nDate:\x20Tue,\x2002\x20Sep\x202025\x2016:16:31\x20GM
SF:T\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en-US\"\x20class=\"theme-a
SF:uto\">\n<head>\n\t<meta\x20name=\"viewport\"\x20content=\"width=device-
SF:width,\x20initial-scale=1\">\n\t<title>Gitea:\x20Git\x20with\x20a\x20cu
SF:p\x20of\x20tea</title>\n\t<link\x20rel=\"manifest\"\x20href=\"data:appl
SF:ication/json;base64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSI
SF:sInNob3J0X25hbWUiOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdX
SF:JsIjoiaHR0cDovL2xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi8vb
SF:G9jYWxob3N0OjMwMDAvYXNzZXRzL2ltZy9sb2dvLnBuZyIsInR5cGUiOiJpbWFnZS9wbmci
SF:LCJzaXplcyI6IjU")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nCont
SF:ent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r
SF:\n400\x20Bad\x20Request")%r(HTTPOptions,197,"HTTP/1\.0\x20405\x20Method
SF:\x20Not\x20Allowed\r\nAllow:\x20HEAD\r\nAllow:\x20GET\r\nCache-Control:
SF:\x20max-age=0,\x20private,\x20must-revalidate,\x20no-transform\r\nSet-C
SF:ookie:\x20i_like_gitea=21ebc1d17db0bf97;\x20Path=/;\x20HttpOnly;\x20Sam
SF:eSite=Lax\r\nSet-Cookie:\x20_csrf=uAInThDzfWInhQq0IXC0SK1C3HM6MTc1NjgyO
SF:Tc5MTI1OTUwMTYwMA;\x20Path=/;\x20Max-Age=86400;\x20HttpOnly;\x20SameSit
SF:e=Lax\r\nX-Frame-Options:\x20SAMEORIGIN\r\nDate:\x20Tue,\x2002\x20Sep\x
SF:202025\x2016:16:31\x20GMT\r\nContent-Length:\x200\r\n\r\n")%r(RTSPReque
SF:st,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plai
SF:n;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Reques
SF:t");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2022|2012|2016 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2022 cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_server_2016
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows Server 2022 (89%), Microsoft Windows Server 2012 R2 (85%), Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.95%E=4%D=9/2%OT=80%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=68B718A1%P=x86_64-pc-linux-gnu)
SEQ(SP=106%GCD=1%ISR=107%TI=RD%II=I%TS=6)
SEQ(SP=106%GCD=1%ISR=10B%TI=I%II=I%SS=S%TS=A)
OPS(O1=M552NW8ST11%O2=M552NW8ST11%O3=M552NW8NNT11%O4=M552NW8ST11%O5=M552NW8ST11%O6=M552ST11)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FFDC)
ECN(R=Y%DF=Y%TG=80%W=FFFF%O=M552NW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=Y%DFI=N%TG=80%CD=Z)

Uptime guess: 0.457 days (since Tue Sep  2 10:50:00 2025)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: Randomized
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| p2p-conficker:
|   Checking for Conficker.C or higher...
|   Check 1 (port 46369/tcp): CLEAN (Timeout)
|   Check 2 (port 56941/tcp): CLEAN (Timeout)
|   Check 3 (port 7147/udp): CLEAN (Timeout)
|   Check 4 (port 53692/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: mean: 0s, deviation: 0s, median: 0s
| smb2-time:
|   date: 2025-09-02T16:16:59
|_  start_date: N/A
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled but not required

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   54.87 ms 10.10.14.1
2   55.05 ms lock.vl (10.129.234.64)

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 21:47
Completed NSE at 21:47, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 21:47
Completed NSE at 21:47, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 21:47
Completed NSE at 21:47, 0.00s elapsed
Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 72.86 seconds
           Raw packets sent: 108 (8.676KB) | Rcvd: 50 (3.136KB)
```
## HTTP (80)

```bash
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-title: Lock - Index
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
```
### Dirsearch

```bash
ashu@kali ~ dirsearch -u http://lock.vl
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/ashu/reports/http_lock.vl/_25-09-02_21-41-11.txt

Target: http://lock.vl/

[21:41:11] Starting:
[21:41:11] 403 -  312B  - /%2e%2e//google.com
[21:41:12] 403 -  312B  - /.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
[21:41:12] 404 -    2KB - /.ashx
[21:41:12] 404 -    2KB - /.asmx
[21:41:13] 500 -    1KB - /.git
[21:41:13] 500 -    1KB - /.git/
[21:41:13] 403 -    1KB - /.git/hooks/
[21:41:13] 403 -    1KB - /.git/info/
[21:41:13] 403 -    1KB - /.git/logs/
[21:41:13] 301 -  159B  - /.git/logs/refs/heads  ->  http://lock.vl/.git/logs/refs/heads/
[21:41:13] 301 -  153B  - /.git/logs/refs  ->  http://lock.vl/.git/logs/refs/
[21:41:13] 301 -  161B  - /.git/logs/refs/remotes  ->  http://lock.vl/.git/logs/refs/remotes/
[21:41:13] 301 -  168B  - /.git/logs/refs/remotes/origin  ->  http://lock.vl/.git/logs/refs/remotes/origin/
[21:41:13] 301 -  154B  - /.git/refs/heads  ->  http://lock.vl/.git/refs/heads/
[21:41:13] 403 -    1KB - /.git/objects/
[21:41:13] 403 -    1KB - /.git/refs/
[21:41:13] 301 -  156B  - /.git/refs/remotes  ->  http://lock.vl/.git/refs/remotes/
[21:41:13] 301 -  163B  - /.git/refs/remotes/origin  ->  http://lock.vl/.git/refs/remotes/origin/
[21:41:13] 301 -  153B  - /.git/refs/tags  ->  http://lock.vl/.git/refs/tags/
[21:41:19] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd
[21:41:21] 404 -    2KB - /admin%20/
[21:41:21] 404 -    2KB - /admin.
[21:41:25] 403 -    1KB - /aspnet_client/
[21:41:25] 301 -  152B  - /aspnet_client  ->  http://lock.vl/aspnet_client/
[21:41:25] 404 -    2KB - /asset..
[21:41:25] 301 -  145B  - /assets  ->  http://lock.vl/assets/
[21:41:25] 403 -    1KB - /assets/
[21:41:26] 403 -  312B  - /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
[21:41:27] 200 -   46B  - /CHANGELOG.TXT
[21:41:27] 200 -   46B  - /CHANGELOG.txt
[21:41:27] 200 -   46B  - /changelog.txt
[21:41:27] 200 -   46B  - /ChangeLog.txt
[21:41:27] 200 -   46B  - /Changelog.txt
[21:41:29] 400 -    3KB - /docpicker/internal_proxy/https/127.0.0.1:9043/ibm/console
[21:41:32] 404 -    2KB - /index.php.
[21:41:32] 404 -    2KB - /javax.faces.resource.../
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/compilerDirectivesAdd/!/etc!/passwd
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/help/*
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/vmLog/disable
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/vmLog/output=!/tmp!/pwned
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/jvmtiAgentLoad/!/etc!/passwd
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/jfrStart/filename=!/tmp!/foo
[21:41:32] 400 -    3KB - /jolokia/exec/java.lang:type=Memory/gc
[21:41:32] 400 -    3KB - /jolokia/read/java.lang:type=*/HeapMemoryUsage
[21:41:32] 400 -    3KB - /jolokia/exec/com.sun.management:type=DiagnosticCommand/vmSystemProperties
[21:41:32] 400 -    3KB - /jolokia/search/*:j2eeType=J2EEServer,*
[21:41:32] 400 -    3KB - /jolokia/read/java.lang:type=Memory/HeapMemoryUsage/used
[21:41:32] 400 -    3KB - /jolokia/write/java.lang:type=Memory/Verbose/true
[21:41:33] 404 -    2KB - /login.wdm%2e
[21:41:38] 404 -    2KB - /rating_over.
[21:41:39] 404 -    2KB - /service.asmx
[21:41:40] 404 -    2KB - /static..
[21:41:42] 403 -    2KB - /Trace.axd
[21:41:42] 404 -    2KB - /umbraco/webservices/codeEditorSave.asmx
[21:41:45] 404 -    2KB - /WEB-INF./
[21:41:46] 404 -    2KB - /WebResource.axd?d=LER8t9aS
```

- No interesting directories
### Vhosts

```bash
bash vhost-fuzzer.sh lock.vl /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://lock.vl 16054

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://lock.vl
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Header           : Host: FUZZ.lock.vl
 :: Header           : User-Agent: PENTEST
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 16054
________________________________________________

:: Progress: [220560/220560] :: Job [1/1] :: 716 req/sec :: Duration: [0:05:27] :: Errors: 0 ::
```

- No VHOST's Found
### Website Features

- Seems to be a static website
- No functionality or features on the main index
## Software Enumeration

- Microsoft IIS httpd 10.0

## SMB (445)

```bash
445/tcp  open  microsoft-ds? syn-ack ttl 127
```

```bash
smbclient -L \\\\lock.vl
Password for [WORKGROUP\ashu]:
session setup failed: NT_STATUS_ACCESS_DENIED
```

## Gitea (3000)

![[Pasted image 20250902220450.png]]

```bash
3000/tcp open  http          syn-ack ttl 127 Golang net/http server
|_http-title: Gitea: Git with a cup of tea
|_http-favicon: Unknown favicon MD5: F6E1A9128148EEAD9EFF823C540EF471
| fingerprint-strings:
|   GenericLines, Help, RTSPRequest:
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest:
|     HTTP/1.0 200 OK
|     Cache-Control: max-age=0, private, must-revalidate, no-transform
|     Content-Type: text/html; charset=utf-8
|     Set-Cookie: i_like_gitea=21c82aaaa9ae2077; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=4O_jVgDrUJdc4Q-33OWhmDwmmPo6MTc1NjgyOTc5MTAwMjgyNDQwMA; Path=/; Max-Age=86400; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 02 Sep 2025 16:16:31 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-auto">
|     <head>
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <title>Gitea: Git with a cup of tea</title>
|     <link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSIsInNob3J0X25hbWUiOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdXJsIjoiaHR0cDovL2xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi8vbG9jYWxob3N0OjMwMDAvYXNzZXRzL2ltZy9sb2dvLnBuZyIsInR5cGUiOiJpbWFnZS9wbmciLCJzaXplcyI6IjU
|   HTTPOptions:
|     HTTP/1.0 405 Method Not Allowed
|     Allow: HEAD
|     Allow: GET
|     Cache-Control: max-age=0, private, must-revalidate, no-transform
|     Set-Cookie: i_like_gitea=21ebc1d17db0bf97; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=uAInThDzfWInhQq0IXC0SK1C3HM6MTc1NjgyOTc5MTI1OTUwMTYwMA; Path=/; Max-Age=86400; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 02 Sep 2025 16:16:31 GMT
|_    Content-Length: 0
| http-methods:
|_  Supported Methods: HEAD GET

```

### Dirsearch

```bash
ashu@kali ~ dirsearch -u http://lock.vl:3000
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/ashu/HackTheBox/Machines/Lock/reports/http_lock.vl_3000/_25-09-02_22-03-50.txt

Target: http://lock.vl:3000/

[22:03:54] 200 -    1KB - /.well-known/openid-configuration
[22:03:54] 200 -  206B  - /.well-known/security.txt
[22:04:02] 200 -   16KB - /administrator/
[22:04:02] 200 -   16KB - /administrator
[22:04:02] 200 -  704B  - /api/swagger
[22:04:09] 200 -   15KB - /explore/repos
[22:04:20] 200 -  279B  - /sitemap.xml
[22:04:23] 200 -   10KB - /user/login/

Task Completed
```

### Software Versions

-  Gitea Version: 1.21.3 
	Powered by Gitea
	Version: 1.21.3
	- A few potential RCEs but they are all authenticated. 

### Exploring `/explore/repos`

![[Pasted image 20250902221154.png]]
- Username Enumeration: `ellen-freeman`
- Public Scripts - `dev-scripts`
