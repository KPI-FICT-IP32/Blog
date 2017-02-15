=======================================
High-Performance Computing Technologies
=======================================

:Lecturer: Yuri Grygorovych Gordienko

.. contents::
   :depth: 3
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
