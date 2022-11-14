---
description: 'Week 3: 9/12/22'
---

# Week 3: DHCP

## Homework - Reading:

The DHCP Server and Routers

* Allows hosts to dynamically obtain its IP address

<figure><img src="https://lh6.googleusercontent.com/Ne_DbY8Lyvaw9U_NmPfe7szfgcnm7HMAj95HSgwEE9SRrwiQHcoryCKCBkl1G4MoSJgLRqF3kokX81qekd7o7whu8m9hcRo6yqGOq_lXVigQYGK3Mtpuurs65O_9zvH5Qng7RAMdYX1Db1bppsJSRFKyr7IV_mTP1zB5ugOjON1ZUCCDj4Hr6uOg36nBPw" alt=""><figcaption></figcaption></figure>

* Above shows a DHCP server setup on a network which has 3 subnets
* The router must be setup in a way that it knows the IP address of the DHCP server
* DHCP must work across routers or through the intervention of BOOTP relay agents
* DHCP DORA (Discover, Offer, Request, Accept)
* DHCP Port Client 68 and Server 67

<figure><img src="https://lh6.googleusercontent.com/FtAiDZ5p3v3SFsFLVWSbI2XuboPq4K5QQ0EO2A3p7-23ix5NuspnWW2avFdrxG0nt2qq1zqpzcq9T8_1UOMNQXFd8UjtuQLfmV5P4A5yCPPAKieA18-sGDZbeTd52Yapur--cgsnjUZcoMd7kYU-RWS7kH40tAbFPs03P1AzVC_F72r78nBoBzEOugiaOQ" alt=""><figcaption><p>DORA</p></figcaption></figure>

<figure><img src="https://lh3.googleusercontent.com/WWaaW10IqFVbq0WLyKQF6R00M-_A05cSb6AoHZJdVV-VOgwmOcJuX9MM_SRhvdPTmwDgVOts5UcZRyt0v3R-mxhaLHfrWkxTV635tN4dFaq2825N4hG6wP1mtg8Ki4j-cg0-QgnYfb3d9cZGjgXu1qDycpfpXD3TlKbTlpaIWApXd467_-cvoLjwjUR1fg" alt=""><figcaption><p>DORA</p></figcaption></figure>

* DHCP options field:
  * Subnet mask
  * Default Gateway
  * Lease Time
  * DNS Server
* Most DHCP servers are configured to let a client reuse a previously allocated IP
  * This can reduce the amount of broadcast traffic
  * A client will broadcast a DHCPREQUEST message on its local subnet.
    * This message will contain a “Requested IP”

## Class:

**DHCP** (Dynamic Host Configuration Protocol)

**What is DHCP?**

* Statically: Manually entered by the administrator (Boo static is for nerds in data centers)
* **Dynamically:** Automatically assigned by the network
* Key information that we need:
  * IP address
  * Subnet mask
  * Default gateway
  * DNS (Domain Name Server)

**How does DHCP Work?**

1. Send out Broadcast (Discover)
   * “I need an IP” - New device
   * Dest IP: 255.255.255.255:68
   * Src IP: 0.0.0.0:67
   * **Broadcast will go out any ports on the VLAN**
2. DHCP Server sends out Offer (Offer)
   * DHCP over different VLANs:
     * Relay Agent (DHCP Relay, DHCP helper) Cisco calls it the IP helper
     * Router needs to know the IP address of DHCP Server
       * This is so it can unicast it and send over the information
       * DHCP server: 192.168.10.100 | Relay Agent: 192.168.10.100
       * Router would forwards as unicast to 192.168.10.100
       * Src of unicast: The Default gateway address for the VLAN
         * This is how the DHCP Server knows where to send the Offer
   * DHCP is like a person lost in new york
   * **DHCP uses UDP**
   * **Server Port: 67**
   * **Client Port: 68**
   * DHCP has two primary Operation Phases:
     * Initialization: Client request
     * Renewal: Client asks to renew its lease
   * Key Fields
     * **Operation Code:**&#x20;
     * **Hardware Type:**
     * **Hardware Length:**&#x20;
   * **DORA**
     * Discover: Client attempts to discover a DHCP server
       * If you spoof Discover you can take all the IP addresses
     * Offer: IP lease offer from the server to client
     * Request: Client requests to use the IP lease sent by the server
     * Acknowledgement: Server sends ack to client that the lease was accepted
     * **Without this process you can have DHCP exhaustion attacks**
   * DHCP snooping
     * Looks at the access port and if one port is asking for more than 1 IP it will shut it down
   * BOOTP: RFC 951
     * Only Discover and Offer
   * **DHCP Renewal**
     * **T1 Renewing:** Process for client to request continued use of its lease
       * This is **50%** through the lease time.
       * Just sends to direct IP adress
         * Using unicast because it knows the IP address of the DHCP server
       * The client sends DHCP Request packets directly to the server
       * If the server responds with a DHCP Ack, the IP lease is renewed and its time clock restarts.
     * If the server doesn’t respond at T1 then it does to T2
     * **T2 Rebinding:** If the server doesn’t respond to the clients renewal requests we eventually reach the rebinding phase
       * This is at **87.5%** through the lease time
       * Gets angry and sends a broadcast to look for another DHCP server
         * So it’s allowed to continue using the same IP
     * **DHCP Expiration:** If nothing responds by the time the lease is over
       * IP goes to a 169.125.4.0
         * Self-assign address
     * **DHCP Relay:**&#x20;
       * Broadcast are Layer 2 only
         * Need a DHCP relay or Helper
           * Picks up broadcast and turns it to unicast and gets it to the DHCP Server
       * **CISCO:**
         * CISCO IOS uses the “ip helper-address”
         * If DHCP server is 10.16.1.50
         * (Config) interface vlan 100
         * (Config-IP) ip helper-address 10.16.1.50
