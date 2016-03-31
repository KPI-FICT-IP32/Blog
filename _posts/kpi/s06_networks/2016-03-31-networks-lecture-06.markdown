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

### TCP. Transmission controll protocol
- TCP protocol **guarantees** data transmission.
- Header size: 20b

### UDP. User datagram protocol.
- Does **NOT** guarantee data transmission
- Header size: 8b

