---
layout: post
title:  "Lecture 9. Routing"
date:   2016-04-28 08:30:00 +0200
categories: kpi_s06_networks
---

One of the Network Layer responsibilities is routing.
Among the data, which is sent, destination IP and source IP are passed over network. This is done to make possible determine sender and reciever. Transport protocol code is also passed in package headers. To make sure that header is OK, CRC checksum is passed in that header (recursion, yup)

# ICMP protocol
Internet control message protocol. This protocol is used for network diagnostics. It works over the Network layer. One of the most well-known features of thisprotocol is ability to check node availability.

TTL -- time to live
Every 3rd level device (like router) decrease TTL by one. If TTL  value is 0, then device drops the packet. Initial TTL value is set by sender. That depends on OS.

RTT -- Round trip time

```
[]---[==]-(+)---(+)---(+)---[]
```

