---
layout: post
title:  "Lecture 3. Physical level."
date:   2016-03-10 08:30:00 +0200
categories: kpi_s06_networks
---

# Lecture 3. Physical level.

OSI levels from 2 (Data link) to 7 (application) are software levels. Developers use them in their software.
The first level (physical) is the trully hardware level.

Physical level generates either electrical/radio/other signals.

Physical level takes incoming frame and encodes it in form of ones an zeros. Then it generates corresponding signals to send this data.

Physical level responsibilities include:

- Data encoding/decoding
- Signaling

### Physical level encodings:

#### NRZ

```
NRZ
|--+   +-----+
|  |   |     |      
|  |   |     |      Uses clocking. One bit sent in one bittime (time unit)
+--+---+-----+-----
  1  0   1  1  0
```

NRZ was used in really slow connections. There is a problem, when several same values come in a sequence (like 4 ones), because it is pretty difficult for receiver to "understand" this data.

#### Manchester coding (the first one)

```
Manchester coding (the first one)
| +--+   ++ +--+    
| |  |   || |  |        
| |  |   || |  |       
+-+--+---++-+--+------
  1  0   1  1  0
```

Change from no signal to existing signal is 1 and from existing signal to no signal is 0. This was much effective than NRZ, but still worked only for slow connections

#### 4B/5B
Every 4bits are encoded in special combination of 5 bits. That allows to avoid issues with several same values in sequence.
Disadvantage: data overhead

#### 8B/10B
The same as 4B/5B, but instead of 4bit and 5bit sequences, 8bit and 10bit are used instead.

## Bandwidth
Bandwidth shows how much data can be sent per some time interval.
It is measured in `bps`(bits per second)

```
1000bps  = 1 kbps
1000kbps = 1 Mbps
1000Mbps = 1 Gbps
1000Gbps = 1 Tbps
```

Bandwidth of Ethernet is 10Mbps

Bandwidth depends on both transmitter and receiver. If transmitter and receiver have different bandwidth, the lowest of them is used.

```
  1Gbps  10Mbps  1Gbps
[]-----[]------[]-----[]
```

Bandwidth in above picture is 10Mbps

### Throughput and goodput
Throughput is the data transmission speed at specific conditions.

```
max:100Mbps  max:100Mbps
[]------{cloud}-----[]
  60Mbps       100Mbps
```
Throughput in above picture is 60Mbps

Goodput is the payload transmission speed at specific conditions. That means, techncal and service data (frame, package, segment, etc) headers are not counted in goodput.

## Connections
- Twisted pair
- Fiber connection
- Wireless
- Coaxial

### Twisted-pair
Twisted-pair has two standards:

- UTP unshielded twisted pair.
- SPT shielded twisted pair.

Max length of Twisted-pair is 100m

Twisted pair consists of 8 wires.

- Orange
- Green
- Blue
- Brown

There are 2 standards:

- T568A
- T568B

|-|---------|---------|
| |  T568A  |  T568B  |
|-|---------|---------|
|1| Green/  | Orange/ |
|2| Green   | Orange  |
|3| Orange/ | Green/  |
|4| Blue    | Blue    |
|5| Blue/   | Blue/   |
|6| Orange  | Green   |
|7| Brown/  | Brown/  |
|8| Brown   | Brown   |
|-|---------|---------|

**Straightthrough twisted-pair:** A-A or B-B
**Crossover twisted-pair:** A-B or B-A

Straighthrough:

 - Switch + PC
 - Switch + Router

Crossover:

 - PC + PC
 - Router + Router
 - Switch + Switch

MDI-x allows us to not bother about which twisted-pair (Straightthrough or crossover) we use.
Only 4 wires are used to transfer data at 100Mbps. Other 4 are used to power devices

### Fiber
2 types:

- Multimod (d = 50-60mkn), up to 1.5km
- Singlemod (d = 9-10mkn), uses laser, up to 80km
