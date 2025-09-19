## The Starting Lab 

![[Pasted image 20250908151201.png]]

```bash
┌──(rootkali)-[~]
└─# cat /etc/hosts
# Your system has configured 'manage_etc_hosts' as True.
# As a result, if you wish for changes to this file to persist
# then you will need to either
# a.) make changes to the master file in /etc/cloud/templates/hosts.debian.tmpl
# b.) change or remove the value of 'manage_etc_hosts' in
#     /etc/cloud/cloud.cfg or cloud-config from user-data
#
127.0.1.1 ip-192-168-100-5.ap-south-1.compute.internal kali
127.0.0.1 localhost

# The following lines are desirable for IPv6 capable hosts
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

```

```bash
┌──(rootkali)-[~]
└─# ip a s                                                                                                                                                                             127 ⨯
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 02:d3:17:d9:f2:cf brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.5/24 brd 192.168.100.255 scope global dynamic eth0
       valid_lft 3083sec preferred_lft 3083sec
    inet6 fe80::d3:17ff:fed9:f2cf/64 scope link 
       valid_lft forever preferred_lft forever

```


## Recon

### Running Netdiscover

```bash
root@kali ~ netdiscover -r 192.168.100.0/24
Currently scanning: Finished!   |   Screen View: Unique Hosts                                                                                                                              
                                                                                                                                                                                            
 7 Captured ARP Req/Rep packets, from 7 hosts.   Total size: 294                                                                                                                            
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.100.1   02:19:54:ee:38:41      1      42  Unknown vendor                                                                                                                           
 192.168.100.50  02:27:be:f6:e1:21      1      42  Unknown vendor                                                                                                                           
 192.168.100.51  02:58:1f:43:ac:b9      1      42  Unknown vendor                                                                                                                           
 192.168.100.52  02:2a:a3:96:12:1d      1      42  Unknown vendor                                                                                                                           
 192.168.100.55  02:40:87:4f:8a:df      1      42  Unknown vendor                                                                                                                           
 192.168.100.63  02:be:6c:4b:3a:9f      1      42  Unknown vendor                                                                                                                           
 192.168.100.67  02:3c:9a:d3:d5:1b      1      42  Unknown vendor   
```
