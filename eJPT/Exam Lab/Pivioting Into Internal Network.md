
```bash
msf6 post(multi/manage/autoroute) > show options

Module options (post/multi/manage/autoroute):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   CMD      autoadd          yes       Specify the autoroute command (Accepted: add, autoadd, print, delete, default)
   NETMASK  255.255.255.0    no        Netmask (IPv4 as "255.255.255.0" or CIDR as "/24"
   SESSION                   yes       The session to run this module on
   SUBNET                    no        Subnet (IPv4, for example, 10.10.10.0)

msf6 post(multi/manage/autoroute) > set SESSION 1
SESSION => 1
msf6 post(multi/manage/autoroute) > set SUBNET 192.168.0.0/24
SUBNET => 192.168.0.0/24
msf6 post(multi/manage/autoroute) > run

[!] SESSION may not be compatible with this module:
[!]  * incompatible session platform: windows
[*] Running module against WINSERVER-03
[*] Searching for subnets to autoroute.
[+] Route added to subnet 192.168.0.0/255.255.255.0 from host's routing table.
[+] Route added to subnet 192.168.100.0/255.255.255.0 from host's routing table.
[*] Post module execution completed
msf6 post(multi/manage/autoroute) > route print 

IPv4 Active Routing Table
=========================

   Subnet             Netmask            Gateway
   ------             -------            -------
   192.168.0.0        255.255.255.0      Session 1
   192.168.100.0      255.255.255.0      Session 1

[*] There are currently no IPv6 routes defined.
msf6 post(multi/manage/autoroute) > use auxiliary/scanner/discovery/arp_sweep 
msf6 auxiliary(scanner/discovery/arp_sweep) > set RHOSTS 192.168.0.0/24
RHOSTS => 192.168.0.0/24
msf6 auxiliary(scanner/discovery/arp_sweep) > run

[+] 192.168.0.2 appears to be up (UNKNOWN).
[+] 192.168.100.50 appears to be up (UNKNOWN).
[+] 192.168.100.51 appears to be up (UNKNOWN).
[*] Scanned 256 of 256 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/discovery/arp_sweep) > show options

Module options (auxiliary/scanner/discovery/arp_sweep):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   INTERFACE                   no        The name of the interface
   RHOSTS     192.168.0.0/24   yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
   SHOST                       no        Source IP Address
   SMAC                        no        Source MAC Address
   THREADS    1                yes       The number of concurrent threads (max one per host)
   TIMEOUT    5                yes       The number of seconds to wait for new data

msf6 auxiliary(scanner/discovery/arp_sweep) > use post/multi/gather/ping_sweep 
msf6 post(multi/gather/ping_sweep) > set RHOSTS 192.168.0.0/24
RHOSTS => 192.168.0.0/24
msf6 post(multi/gather/ping_sweep) > run
[-] Post failed: Msf::OptionValidateError One or more options failed to validate: SESSION.
msf6 post(multi/gather/ping_sweep) > show options

Module options (post/multi/gather/ping_sweep):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOSTS   192.168.0.0/24   yes       IP Range to perform ping sweep against.
   SESSION                   yes       The session to run this module on

msf6 post(multi/gather/ping_sweep) > set SESSION 1
SESSION => 1
msf6 post(multi/gather/ping_sweep) > run

[*] Performing ping sweep for IP range 192.168.0.0/24
[+]     192.168.0.1 host found
[+]     192.168.0.57 host found
[+]     192.168.0.51 host found
[+]     192.168.0.50 host found

```

## TARGET 1: `192.168.0.51`

## TARGET 2: `192.168.0.57`

