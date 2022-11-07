---
description: Internet Protocol Security
---

# IPSEC Site-to-Site VPN

### Base Setup:

The {access\_list\_#} must be greater than 100

```
! Identify traffic to send through tunnel with access-list
access-list {access_list_#} permit ip {src_net} {src_mask_wildcard} {dst_net} {dst_mask_wildcard}
! Configure IKE Phase 1 ISAKMP Policy on Router
crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit
crypto isakmp key {KEY} address {public_ip_of_other_router}
! Configure the IKE Phase 2 IPsec policy
!- Create the transform-set "VPN-SET"
crypto ipsec transform-set VPN-SET esp-aes esp-sha-hmac
!- Create the crypto map "VPN-MAP"
crypto map VPN-MAP 10 ipsec-isakmp
description VPN connection to {peer_router_name}
set peer {public_ip_of_other_router}
set transform-set VPN-SET
match address {access_list_#}
exit
! Configure the "crypto map" on the outgoing interface.
interface {interface} {interface_#}
crypto map VPN-MAP
```

### Example:

```
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

### Notes:

To see if the VPN is working:

```
enable
show crypto ipsec sa
```
