---
layout: post
title:  "Lecture 4. Fiber. Wireless. Application level"
date:   2016-03-17 08:30:00 +0200
categories: kpi_s06_networks
---

# Lecture 4.

### Fiber

Fiber cable usually uses two fiber wires: one wire to transmit data in one direction
There are one-wire fiber cables. These cables use light waves with different wave length

Two types of connector:

LC FC
SC

#### Ports

- GBIC - old format
- SFP (1 Gbps)
- SFP+ (10 Gbps)
- QSFP (40Gbps)
- QSFP+ (80Gbps)

Connection speed can be increased using **link aggregation**: two cables on the software level recognized as one link, and balancer sends part of packets on the one cable, and part -- on another cable.

### Wireless
802.11 standard. 

|  standard name   |  frequency   |      speed     |
|------------------|--------------|----------------|
|standard 802.11a  | 2.4Ghz       | up to 11 Mbps  |
|standard 802.11b  | 5Ghz         | up to 52 Mbps  |
|standard 802.11g  | 2.4Ghz       | up to 52 Mbps  |
|standard 802.11n  | 2.4Ghz, 5Ghz | up to 300 Mbps |
|standard 802.11ac | 2.4Ghz, 5Ghz | > 1 Gbps       |

2.4 Ghz is used by wide variety of devices, hence if there is another device which works on this frequency nearby, the major loss of quality will occur due to signal interference.

# Application level
Main protocols:

- HTTP
- DNS 
- DHCP
- FTP
- telnet
- SSH
- IMAP
- POP3
- SMTP

Client/Server architecture
Peer-to-peer (P2P)

**FTP**
Data transfered in a plain form. No encryption.

**DHCP**
Dynamic host configuration protocol.

1. Client broadcasts request to receive IP address (DHCP-discover)
2. DHCP server finds accessible ip addresses and returns DHCP-offer.
3. Client receives DHCP-offer and broadcasts its intent to use offer. (DHCP-Request)
4. Corresponding DHCP server registers client and returns DHCP-Acknowledge response to client
5. Client saves received IP address
