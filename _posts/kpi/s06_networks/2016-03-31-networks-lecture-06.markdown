---
layout: post
title:  "Lecture 6. Transport layer."
date:   2016-03-31 08:30:00 +0200
categories: kpi_s06_networks
---

# Transport level

PDU: Segment

- **data exchange between applications**. It does not matter, where the application is, it only matters which application. So transport level does not transmits data between hosts, it only determines which data belongs to which application and passes data from/to corresponding application.
- splits data into small parts (chunks)
- determines, which application received data belongs to
- message tracking
- flow controll.


## Message  passing on transport level

1. Ordering received messages
2. Reliability. Wait for transmission confirmation.
3. Flow controll. Message will be transfered in batches (several parts transmitted at a time)
4. Segmentation.

## Protocols

Dependeing on protocol specific header is added to message.
In both TCP and UDP application identifier is passed in header. 2b is used to store this application id. Hence there are 2^16 unique identifiers **(ports)**.

Ports from 0 to 1023 are called *well-known*
Ports from 1024 to 49151 are called *registered ports*. Use these ports when you develop your app
Ports from 49152 to 65535 are *Dynamic* ports

|Protocol|Port  |Transfer protocol                                          |
|--------|------|-----------------------------------------------------------|
|FTP     |20,21 |TCP                                                        |
|SSH     |22    |TCP                                                        |
|TELNET  |23    |TCP                                                        |
|SMTP    |25    |TCP                                                        |
|DNS     |53    |UDP (when client requests data), TCP (to sync DNS servers) |
|DHCP    |67,68 |UDP                                                        |
|HTTP    |80    |TCP                                                        |
|POP3    |110   |TCP                                                        |
|IMAP    |143   |TCP                                                        |


Within header both source and destination ports are passed.

```
 SRC PORT   DST PORT       DATA 
+---------+----------+-------------+
|  50000  |    80    |             |
+---------+----------+-------------+
```

### TCP. Transmission controll protocol
- TCP protocol **guarantees** data transmission.
- Header size: 20b

```
|16b   SRC PORT|16b   DST PORT|
|6b:flags|                    |
|32b: ISN                     |
```

- Before data transmission source and destination establish TCP connection (3-wave handshake):

```
|                      |
|------SYN,seqa------->|
|                      |
|<---SYN,ACK(seqb)-----| If there is nothing on this port RST returned instead
|                      |
|----ACK(seqb + 1)---->| Now we have TCP connection established
|                      |
|                      |
|                      |
|---DATA(1602)-------->| Data size passed within seq param. 1602 is size here
|                      |
|<---ACK(1603)---------| Data transfer ackknowledge.
|                      |
|                      |
|-----FIN------------->| A sent all data and wants to finish connection
|<----FIN--------------| B wants to finish connection too
|-----ACK------------->| Confirm connection end
A                      B
```

flags: SYN, ACK, RST, FIN, PUSH, URG

- TCP tries to send more data with every sequential request. I.E. within first transfer it sends 1kb. Then 2, 4,8,16 and so on and so forth. (flow control)

    use `netstat`


### UDP. User datagram protocol.
- Does **NOT** guarantee data transmission
- Header size: 8b

