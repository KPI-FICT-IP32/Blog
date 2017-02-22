=======================================
High-Performance Computing Technologies
=======================================

:Lecturer: Yuri Grygorovych Gordienko

.. contents::
   :depth: 4
..

--------------


Lecture 1. Introduction
=======================

date: Wed Feb 15 13:47:01 EET 2017

Historical info
---------------

Parallel processing cannot be replaced with the sequential
one because of `Moore' Law <https://en.wikipedia.org/wiki/Moore's_law>`_

  Number of transistors in a dense integrated circuit 
  doubles approximately every two years.

.. note::

  See also a 
  `Kurzweil's extension of Moore's law <http://www.kurzweilai.net/the-law-of-accelerating-returns>`_

Storage law
  storage capacity increases 2x every 12 months

Gilder's law
  network (optical) bandwidth increases 2x every 9 months

Distributed computing
  a collection of independent computers that appears to its users
  as a single coherent system 

Lesslie Lamport' test for distributed system

  You know you have a distributed system when the crash of a computer
  you've never heard of stops you from getting any work done


Differences between parallel and distributed systems
----------------------------------------------------

+--------------+-------------+--------------+
| Criteria     | Parallel    | Distributed  |
|              | System      | System       |
+==============+=============+==============+
| Connectivity | Tightly     | Loosely      |
|              | coupled     | coupled      |
+--------------+-------------+--------------+
| Memory       | Uses shared | Uses message |
| access       | memory      | passing as   |
|              | to exchange | each CPU has |
|              | information | its own      |
|              |             | memory       |
+--------------+-------------+--------------+
| Granularity  | Finer       | Coarse       |
|              | grained     | grained      |
+--------------+-------------+--------------+


Usages
------

- Strategic systems
- Visualisation and Graphics
- Economics and Finance
- Scientific computing

  - Physics (LHC)
  - Bioinformatics (protein-docking)
  - Geology (seismography)
  - Astronomy (simulation of galaxy)

Models
------

Distributed computations are characterised with models.

- Architectural models
  
  `Flynn's taxonomy <https://en.wikipedia.org/wiki/Flynn's_taxonomy>`_
  distinguishes the following categories:

  - **SISD**: traditional uniprocessor computers
  - **MISD**: Space shuttle flight control computer
  - **SIMD**: array processor, GPU
  - **MIMD**: parallel and distributed systems

  There are different architectural-service models as well:

  - Centralised (mainframe, cluster)
  - Client-server (mail, banking, computations)
  - Multi-tier (grid, DNS)
  - Peer-to-peer (file exchange, computations)
  
- Interaction models

  Interaction models give answers to the following questions:

  - How do we handle time?
  - Are there time limits?

  There are two major models:

  - Synchronous
  - Asynchronous

- Fault models

  The crucial question here is:
    
    What kind of faults can occur

  - Omission faults (a processor or communication fails to perform it is supposed to do)
  - Timing faults (in synchronous distributed systems)
  - Arbitrary faults (WTF has happened?)

Distributed computing
---------------------

Advantanges
~~~~~~~~~~~

- Performance
- Reliability
- Distribution
- Incremental growth
- Sharing computation/data/resources/management
- Communication
- Economics
- Flexibility

Disadvantages
~~~~~~~~~~~~~

- Heterogeneity (hardware, software, operation, etc)
- Software development
- Networking
- Incremental growth (scalability is a pain)

Pitfals
~~~~~~~

- The network is **NOT** reliable
- The network is **NOT** secure
- The network is **NOT** homogeneous
- The topology is **NOT** constant
- Latency is **NOT** zero
- Bandwidth is **NOT** infinite
- Transport cost is **NOT** zero
- There is **NO** single administrator

Design
~~~~~~

Main charachteristics:

- Transparency
  
    How to make impression that the collection of machines is a "simple" single computer?

  - Access
  - Location
  - Migration
  - Replication
  - Concurrency
  - Failure
  - Performance
- Scalability
- Performance

  - Performance of individual workstations
  - Speed of the communication infrastructure
  - Extent of reliability
  - Flexibility in workload allocations (i.e. idle processors 
    should be allocated automatically to a user's task)
- Heterogeneity

  - different hardware
  - different software
  - various devices (PCs, mobiles, ATM-machines, sensors, etc)
  - diverse networks and protocols

Cluster and Grid computing
--------------------------

:Cluster computing:
  collection of high-end computers usually
  closely connected through LAN

- Homogeneous: OS, hardware
- Work: together like a single computer
- Applications are hosted on one machine and user machines connect to it.
  Clients connect via terminals

`High-performance computing center at KPI <http://hpcc.kpi.ua>`_

:Grid computing:
  collection of clusters, which may be combined in a "GRID"
  of a massive computing power

- Heterogeneous
- Work: for collaborations grids use virtual organizations
