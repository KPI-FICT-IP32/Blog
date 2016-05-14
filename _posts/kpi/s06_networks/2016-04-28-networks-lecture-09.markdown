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

# Routing

## WTF is router? (+)

> Router is a box with holes, buttons, wires and light indicators. It is some sort of computer, without monitor. There are CPU, RAM, NVRM, ROM, physical interfaces, etc...

Router is a 3rd level device. That means, it works on 3rd (Network) layer.

Despite everything else router allows us to unite different networks with each other, find best path to some host, and so on and so forth.

## Routing table
Every router stores routing table. Routing table stores records of networks, next-hop or interfaces, where the network is.

There are 3 types of records in routing table:

1. **Directly connected.** It appears as soon as router is enabled or device is plugged into network/router
2. **Static routes.** System administrators/users fill these records. 
3. **Dynamic routes.** These records are populated by routers themselves, depending on their configurations.

## Rules of routing

1. If you have a route on one router in netwrok, it does not mean other ruoters have that route.
2. If you create a route, you have to create a backward one
3. Next-hop **must** be in directly-connected network

## Static routes

> **WARNING** I've messed upo this topology. PLS FIX IT!

```
                 192.168.2.0/24
                       ___
                        |
                        |
 R1. 192.168.4.0/30     |192.168.5.0/30        192.168.3.0/24
    (+)i2------------i1(+)i2-----------------------(+) R3.
  i1+.254              R2.                          |
   /                                              [==]----[]
 \\
  192.168.1.0/24
```


### R1
192.168.1.0/24 | i1
192.168.4.0/30 | i2
192.168.3.0/24 | 192.168.4.2

192.168.3.0/24  next-hop 192.168.4.1

### R2
192.168.4.0/30 | i1
       .2.0/24 | i3
       .5.0/30 | 
       .3.0/24 | 192.168.5.2
