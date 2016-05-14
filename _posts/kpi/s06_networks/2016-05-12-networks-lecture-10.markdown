---
layout: post
title:  "Lecture 10. Dynamic routing"
date:   2016-05-12 08:30:00 +0200
categories: kpi_s06_networks
---

# Lecture 10. Dynamic routing

```
                R2
            ----(+)-| B
      R1   /     |
A |---(+)--      |
           \     |
            ----(+)-| C
                R3
```

There are some running processes on routers. They exchange some data, which allow to build routing tables for networks.

Chief weaponry of dynamic routing protocols include such diverse things as

 - Messages
 - Path finding algorithms
 - Corresponding data structures

## Comparisson of static and dynamic routing

| Criteria | Static | Dynamic |
|----------|--------|---------|
| Scaleability | Bad: network must be reconfigured manually to scale | **Good** |
| Knowledges | **Little knowledge** | A lot of knowledge required |
| CPU, resourses | **Minimal** | Uses CPU to configure routing |
| Reconfiguration | Complex | **Simple** |
| Security | Good | **Bad** |
| Fault tolerance | Extremely bad | **Good (depends on used protocol)** |

## Routing configuration protocols canbe divided into two groups:

- **IGP** Interior gateway protocol
- **EGP** Exterior gateway protocol

**Autonomic system** is a group of networks running under a single administrative control. This could be our company or a branch of company. Just like Subnetting AS is also used to break a large network in smaller networks.

## Classification

- EGP
  - [BGP](https://en.wikipedia.org/wiki/Border_Gateway_Protocol)
- IGP
  - distance-vector
    - [RIP](https://en.wikipedia.org/wiki/Routing_Information_Protocol)
    - [IGRP](https://en.wikipedia.org/wiki/Interior_Gateway_Routing_Protocol)
    - [EIGRP](https://en.wikipedia.org/wiki/Enhanced_Interior_Gateway_Routing_Protocol)
  - link-state
    - [IS-IS](https://en.wikipedia.org/wiki/IS-IS) (Intermediate system to intermediate system)
    - [OSPF](https://en.wikipedia.org/wiki/Open_Shortest_Path_First) (Open shortest path first)

Distance-vector protocol know nothing but the next hop and some metric, called distance.

Link-state protocols try to build a full network topology graph and then find paths on that graph.

## RIP =(

```
  A   R1   B  R2   C  R3   D
|-----(+)-----(+)-----(+)-----|
```

|R1         |R2         |R3          |
|-----------|-----------|------------|
|A - 0      |B - 0      |C - 0       |
|B - 0      |C - 0      |D - 0       |
|-----------|-----------|------------|
|_C: R2 - 1_|_D: R3 - 1_|_B: R2 - 1_ |
|           |_A: R1 - 1_|            |

Every 30 seconds routers broadcast their routing table to their "neighbours".

Metrics:

| Metric      | Protocol |
|-------------|----------|
| Hop count   | RIP      |
|-------------|----------|
| Bandwidth   | EIGRP    |
| Delay       | EIGRP    |
| Load        | EIGRP    |
| Reliability | EIGRP    |
|-------------|----------|
| Cost        | OSPF     |

If there are several paths with the same metrics, RIP (as well as any other protocol) will balance traffic among these pathts.

Maximum diameter of network, to which RIP can be applied is **15**

**Split horizont**. If router R2 received path to D from R3, it will not send recieved path (D) to R3.
