# Lab 10-1: IPSEC Packet Tracer 1

### Summary

The goal of this lab is to setup an IPSEC Site-to-Site VPN between Champlain and Middlebury.

### Subnet Table

| Name               | Network Address | Subnet        | Default Gateway |
| ------------------ | --------------- | ------------- | --------------- |
| VTEL to Champlain  | 216.93.144.0    | 255.255.255.0 | 216.93.144.1    |
| VTEL to Middlebury | 140.230.18.0    | 255.255.255.0 | 140.230.18.1    |
| Champlain Private  | 172.16.84.0     | 255.255.255.0 | 172.16.84.1     |
| Middlebury Private | 192.168.28.0    | 255.255.255.0 | 192.168.28.1    |

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Network Photo</p></figcaption></figure>

### Steps:

#### Servers

Configure both servers to have proper gateway and IP address.

#### Champlain router

```
enable 
conf t
hostname champlain-router
! Interface setup for VTEL to Champlain
interface FastEthernet 0/0
ip address 216.93.144.2 255.255.255.0
no shutdown
! Interface setup for internal Champlain
interface FastEthernet 0/1
ip address 172.16.84.1 255.255.255.0
no shutdown
ip route 0.0.0.0 0.0.0.0 216.93.144.1
! Identify traffic to send through tunnel with access-list
access-list 101 permit ip 172.16.84.0 0.0.0.255 192.168.25.0 0.0.0.255 
! Configure IKE Phase 1 ISAKMP Policy on Champlain Router
crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit
crypto isakmp key NET330 address 140.230.18.2
! Configure the IKE Phase 2 IPsec policy
!- Create the transform-set "VPN-SET"
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac
!- Create the crypto map "VPN-MAP"
crypto map VPN-MAP 10 ipsec-isakmp
description VPN connection to Middlebury
set peer 140.230.18.2
set transform-set VPN-SET
match address 101
exit
! Configure the "crypto map" on the outgoing interface.
interface FastEthernet 0/0
crypto map VPN-MAP

```

#### Middlebury Router

```
enable 
conf t
hostname middlebury-router
! Interface setup for VTEL to Middlebury
interface FastEthernet 0/0
ip address 140.230.18.2 255.255.255.0
no shutdown
! Interface setup for internal Champlain
interface FastEthernet 0/1
ip address 192.168.25.1 255.255.255.0
no shutdown
ip route 0.0.0.0 0.0.0.0 140.230.18.1
! Identify traffic to send through tunnel with access-list
access-list 101 permit ip  192.168.25.0 0.0.0.255 172.16.84.0 0.0.0.255 
! Configure IKE Phase 1 ISAKMP Policy on Middlebury Router
crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit
crypto isakmp key NET330 address 216.93.144.2
! Configure the IKE Phase 2 IPsec policy
!- Create the transform-set "VPN-SET"
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac
!- Create the crypto map "VPN-MAP"
crypto map VPN-MAP 10 ipsec-isakmp
description VPN connection to Champlain
set peer 216.93.144.2
set transform-set VPN-SET
match address 101
exit
! Configure the "crypto map" on the outgoing interface.
interface FastEthernet 0/0
crypto map VPN-MAP
```

#### VTEL

```
enable
conf t
hostname vtel-router
! Interface setup for VTEL to Champlain
interface FastEthernet 0/0
ip address 216.93.144.1 255.255.255.0
no shutdown
! Interface setup for VTEL to Middlebury
interface FastEthernet 0/1
ip address 140.230.18.1 255.255.255.0
no shutdown
```
