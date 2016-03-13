---
layout: post
title:  "Lecture 2. Network design. Network models."
date:   2016-02-25 08:30:00 +0200
categories: kpi_s06_networks
---

# Lecture 2. Network design. Network models.

## Network design

There are 4 characteristics of well-designed network. Here they are: 

- **Redundancy**
- **Scalability** -- Network have to be easy to extend witout modifying existing parts of the network
- **QaS (Quality of Service)** -- Crucial data must have priority over other data
- **Security**

In the future lectures network topology illustrations will be used.

**Legend:**

> End devices: `[] Generic, [L] Laptop, [S] Switch`
>
> Intermediate devices: `[==] Switch, (+) Router, \(+)/ Wifi router`

When messages are too big, they are split into smaller parts.  This is called **multiplexing**. Packets are enumerated. This allows to restore a whole message from parts

```
[]--------[==]--(+)
         / |
        /  |
[]-----/   |
           |
           |
 LAN       []
```

Network types:

- **LAN** -- Local Area Network
- **WAN** -- Wide Area Network
- **Internet**


## Network models
Standard developers:
- IEEE Institute of electric and electronics engineering
- IETF Internet engineering task force

Protocols are described in documents called *RFC*

### TCP/IP Model

| № | Name                    |
|---|-------------------------|
| 4 | Application             |
| 3 | Transport               |
| 2 | Internet                |
| 1 | Network access          |

### OSI Model (developed by ISO)

| № | Name                    |
|---|-------------------------|
| 7 | Application             |
| 6 | Presentation            |
| 5 | Session                 |
| 4 | Transport layer         |
| 3 | Network                 |
| 2 | Data link               |
| 1 | Physical                |

- Application layer is the layer which is used by user applications
- Presentation layer-- data encoding, compressing, etc
- Session layer -- ??
- Transport layer -- transferring data between applications
- Network layer -- transfering data between devices
- Data link -- interface between application and hardware layers
- Physical layer -- hardware level

Each protocol has its own PDU (Protocol data unit).

| Level(s)| PDU     |
|---------|---------|
| 7, 6, 5 | Data    |
| 4       | Segment |
| 3       | Packet  |
| 2       | Frame   |
| 1       | Bytes   |
