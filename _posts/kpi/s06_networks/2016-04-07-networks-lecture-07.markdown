---
layout: post
title:  "Lecture 7. Network layer. IPv4"
date:   2016-04-07 08:30:00 +0200
categories: kpi_s06_networks
---

# Network layer

In addition to data encapsulation and decapsulation which occur on every layer, network layer is also responsible for addressing devices and routing.

Network layer protocols include

- IPv4
- IPv6

Network layer is fully unreliable. You cannot be sure if the data will be sent/received.

Network layer protocols are unaware of data transmission method (wifi, ethernet, smth else) used at physical layer.

# Nets and subnets

```
    [ ]-  -[ ]
        \/
 [ ]----------[ ]
        /\
    [ ]-  -[ ]

This how it used to be earlier
```

But now there are so many devices that having one net for all of them is not enough.
Here subnets are coming for rescue.

There are different ways of distributing subnets (or splitting net into subnets)

- **geographical.** This is the dummiest way. I.E. one floor in 10-floor building has its own subnet.
- **purpose.** Some people (finance dpt) need high reliable conection for work and other (managers) does not. We can create subnets for every group of peopple with specia configuration
- **security.** Sometimes for security reasons we need to restrict access for different groups of devices. Subnets for the rescue.

```

   [ ]-              -[ ]
       \            /
 [ ]---[=]---(+)---[=]---[ ]
       /            \
   [ ]-              -[ ]

Now we have two subnets =)
```

Gateway is used to communicate between subnets.

## Addressing

Sample IPv4 address: `193.47.196.75`. IPv4 address' length is 32bits (4 octets). It consists of 4 bytes splitted with dots.

IP address consists of two parts: 

- Network part
- Host part

```
193.47.196.75  /24
----------|----|----
Network   |Host|Prefix
part      |part|
```

Prefix determines how many bits are used for network part
To determine IP address of network we have to fill host part of IP address with zeros.
To get broadcast address we have to fill host part of IP address with ones. (bits)

|Address type | IP address        |
|-------------|-------------------|
|Host IP      | 192.47.196.75/24  |
|Network IP   | 192.47.196.0/24   |
|Broadcast IP | 192.47.196.255/24 |

Number of available hosts in network is:

```
     n
N = 2  - 2

N -- number of available hosts in network
n -- length of the host part in bits (32 - prefix)
```

### IPv4 address classification:

```
| Class | IP address range           |Prefix| Note                           |
|-------|----------------------------|------|--------------------------------|
|   A   |  1.0.0.0 -- 127.255.255.255| /8   | These networks were given to   |
|   B   |128.0.0.0 -- 191.255.255.255| /16  | big organizations as there are |
|   C   |192.0.0.0 -- 223.255.255.255| /24  | a lot of available hosts       |
|-------|----------------------------|------|--------------------------------|
|   D   |224.0.0.0 -- 239.255.255.255|      | Multicast addresses            |
|   E   |240.0.0.0 -- 255.255.255.255|      | Reserved addresses             |
```

There are some reserved addresses:

- 127.0.0.0/8 -- localhost
- 169.254.0.0/16 -- M$ addresses used in networks w/o DHCP
- 192.0.52.0/24 -- WTF is this?
- 0.0.0.0
- 255.255.255.255 -- network broadcast address

Addresses can be either public or private. Private addresses are used in private networks and are unaccessible from Internet.

Private addresses lay in the following ranges:

- 10.0.0.0/8
- 172.16.0.0/12 -- 172.31.255.255/12
- 192.168.0.0/16

### NAT
NAT stands for Network address translation. This topic will be covered after test will be passed.
This is used to give Internet access for devices which obtain private IPv4 address

## Message types:

There are three _main_ types of messages:

1. **Unicast**. Only one host is the recipient of mesage. 
2. **Broadcast**. Message is sent to every available host in the broadcast domain. One broadcast domain is equal to one subnet. Broadcast messages do not pass through layer-3 devices.
3. **Multicast**. Multicast messages are sent to specified group of devices.
4. **Anycast**. Messages are routed to the topologically nearest node in a group of potential receivers, though it may be sent to several nodes, all identified by the same destination address.
5. **Geocast**. Message is sent to a group of destinations in a network identified by their geographical locations. It is a specialized form of multicast addressing used by some routing protocols for mobile ad hoc networks.
