# Lab 11-1:  Access-Lists

## Summary

During this lab we used a PT activity to learn more about Access-Lists and how they operate.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Network Diagram</p></figcaption></figure>

## Setup

### Router 3 block traffic inbound from 192.168.11.0/24

```
!- must do enable and password by hand
config t
ip access-list standard STND-1
deny 192.168.11.0 0.0.0.255
permit any
exit
interface serial 0/0/0
ip access-group STND-1 in
```

### Router 2 outbound block 192.168.10.0/24 to 200.200.200.1

```
!- must do enable and password by hand
config t
ip access-list extended EXTEND-1
deny ip 192.168.10.0 0.0.0.255 host 200.200.200.1
permit ip any any
exit
interface serial 0/0/0
ip access-group EXTEND-1 out
```

### Router 1 deny all access from ISP to File Server 200.200.200.0/30 to 192.168.20.210

```
!- must do enable and password by hand
config t
ip access-list extended FILE-1
deny ip 200.200.200.0 0.0.0.3 host 192.168.20.210
permit ip any any
exit
interface serial 0/2/0
ip access-group FILE-1 in
```

### Router 1 only web access to the web server 0.0.0.0 0.0.0.0 to 192.168.20.201 eq www

```
!- must do enable and password by hand
config t
ip access-list extended Web-1
permit tcp any host 192.168.20.201 eq www
exit
interface FastEthernet 0/0
ip access-group Web-1 out
```
