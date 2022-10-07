# Lab 4.2: Small Enterprise-Class Lab

### Summary

During this lab we built on DHCP and VLAN confirmation as well added a bit of DNS knowledge. Very fun lab all around.

### Subnet Table

| Network Name / VLAN | Hosts Needed | Network   | Subnet           | Router Address | Usable Range          | DHCP Range              |
| ------------------- | ------------ | --------- | ---------------- | -------------- | --------------------- | ----------------------- |
| Clinic (10)         | 300          | 10.15.0.0 | 255.255.254.0/23 | 10.15.0.1      | 10.15.0.2-10.15.1.254 | 10.15.1.100-10.15.1.254 |
| Vistor (20)         | 300          | 10.15.2.0 | 255.255.254.0/23 | 10.15.2.1      | 10.15.2.2-10.15.3.254 | 10.15.3.100-10.15.3.254 |
| Office (30)         | 300          | 10.15.4.0 | 255.255.254.0/23 | 10.15.4.1      | 10.15.4.2-10.15.5.254 | 10.15.5.100-10.15.5.254 |
| Counseling (40)     | 150          | 10.15.6.0 | 255.255.255.0/24 | 10.15.6.1      | 10.15.6.2-10.15.6.254 | 10.15.6.100-10.15.6.254 |
| Default (1)         | 150          | 10.15.7.0 | 255.255.255.0/24 | 10.15.7.1      | 10.15.7.2-10.15.7.254 | 10.15.7.100-10.15.7.254 |

### Starting File and Finished File

<figure><img src="../.gitbook/assets/Screenshot 2022-09-23 193449.png" alt=""><figcaption><p>Starting File</p></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2022-09-23 193552.png" alt=""><figcaption><p>Finished File</p></figcaption></figure>

### Assigning IP helper addresses

1. Enter the `CLI` for a MLS
2. In `(config)` mode type `interface vlan {VLAN-ID}`
3. Then type `ip helper-address {IPaddr-DHCP-Server}`
4. Type `exit`
5. Repeat steps 2 to 4 for the rest of the VLANs

### DNS Setup

1. Click `Serivces` Tab
2. Select `DNS`
3. `Name` is the DNS record you want to set.&#x20;
4. Then set `Type` [Resources for DNS Types and Queries](https://ns1.com/resources/dns-types-records-servers-and-queries)

#### DNS Setup Example

<figure><img src="../.gitbook/assets/Screenshot 2022-09-23 193937.png" alt=""><figcaption><p>DNS Config</p></figcaption></figure>

### Side Notes

DON'T FORGET TO TURN ON VLAN 1

1. `interface vlan 1`
2. `no shutdown`
