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

Lecture 2. Parallel computing
=============================

Parallel computing
  a form of computuation in which many calculations are carried out simultaneously.

There are different levels of parallel computing:

  - Instruction

    a single operation of a processor
  - Thread

    stream of execution (has one or multiple instructions)
  - Task
  - Process

Level of parallel computing

 - Task level
 - Instruction level
 - Bit level

Classification of system
------------------------

- Flynn's taxonomy
- Memory access

  - shared memory
    - centralized (SMP)
    - distributed (NUMA)
  - individual memory
    - distributed

UMA (Uniform memory access)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

- equal acccess rights
- equal memory access time

NUMA
~~~~

- usually physically linked 2 or more SMPs so they can access mem of each other directly
- Not all have eq access time
- Memory acces across the link is much slower

Distributed
~~~~~~~~~~~

- Each CPI has its own local mem and changes are not visible to other CPUs
- Processors are connected by network
- Program must define a way to transfer data between processors

Massively parallel processors
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MPP architecture consists of nodes each having its own processor, memory and I/O subsystem

Programming models
------------------

Programming Model
  some model which represents an abstraction of the computer system and enables the expression of
  ideas in some form

- Shared model

  - Processors read write the variables stored in a shared address space asynchronously
  - Access to the shared memory is controlled by some mechanisms (locks/semaphores)

- Threads model
- Data parallelization
- Message Passing


+--------------------+---------------+------------------------+
| Aspect             | Shared memory | Message passing        |
+====================+===============+========================+
| Communication      | Implicit      | Explicit mesages       |
+--------------------+---------------+------------------------+
| Synchronization    | Explicit      | Implicit (via message) |
+--------------------+---------------+------------------------+
| Hardware support   | Typically     |                        |
|                    | required      | None                   |
+--------------------+---------------+------------------------+
| Development effort | Lower         | Higher                 |
+--------------------+---------------+------------------------+
| Tuning Effort      | Higher        | Lower                  |
+--------------------+---------------+------------------------+

Implementation of parallelism
-----------------------------

Load balancing
~~~~~~~~~~~~~~

To ditribute work among all tasks so they are all kept busy all of the time

Ways to achieve:

- Adequate partitioning
- Dynamic work assignment
  - Scheduler/task-pool
  - Algorithm to detect and handle imbalances

.. note::

  If barrier synchronization is used then the slowest task determines the
  time of execution

Granularty
~~~~~~~~~~

computation/communication ratio

:Fine grained parallelism: 

  **few** computation events are done between communication events

  - High communication overhead
  - Small opportunity to enhance performance

:Coarse-grain parallelism: 

  **many** computational events are done between communication events.

  - Large opportunity to enhance performance
  - Harder to do load balancing efficiently

Amdahl's law
------------

- Suppose that the sequential execution of a program takes :math:`T_1` time units
  and the parallel execution on :math:`p` processors takes :math:`T_p` time units
- Suppose that out of the entire execution of the program, :math:`s` fraction of it
  is not parallelizable while :math:`1-s` fraction is parallelizable
- Then the speedup:

  .. math::
    
      \frac{T_1}{T_p} = \frac{T_1}{T_1 \cdot s + T_1 \cdot \frac{1 - s}{p}} 
                      = \frac{1}{s + \frac{1 - s}{p}}

.. note::

  - Amdahl's Law is too simple for real cases
  - The communication overhead and workload balance among processes (in general) should 
    be taken into account

There are other Laws of paralel computing performance:

- Gustafsons Law (1988)
    another way to evaluate the performance of a parallel program
- Karp/Flat Metric (1990)
    whether the principle barrier to the program speedup is the amount of inherently
    sequential code or parallel overhead
- Isoefficiency (isogranularity) metric
    the scalability of a parallel algorithm executing on parallel systems

Performance guidelines
----------------------

- Maximize the fraction of our program that can be parallelized
- Balance the workload of parallel processes
- Minimize the time spent for communication


Lecture 3. Metrics
==================

- Time
- Speedup

  .. math::

     Speedup = \Psi(n,p) = \frac{\text{sequential execution time}}{\text{parallel execution time}}
             = \frac{t_s}{t_p}


- Efficiency

  measure of processor utilisation as the speedup divided by the number of processors

  .. math::

     Efficiency = \varepsilon(n,p) = \frac{\text{Speedup}}{\text{Processors}}

  Note that

  .. math::
      \text{speedup} \leq \text{processors}

  Since :math:`\text{speedup} \geq 0` and :math:`\text{processors} > 1`, it follows that

  .. math::
     
    0 \leq \varepsilon(n,p) \leq 1

  However there are **superlinear** algorithms, when

  .. math::
    
     \text{speedup} > \text{processors}

  and for this case 

  .. math::
    
    \varepsilon(n,p) > 1

- Cost 

  .. math::

     \text{cost} = \text{parallel running time} \cdot \text{processors}


Types of computing problems
---------------------------

:Embarassingly parallel problem:
  is one for which little or no effort is required to separate the problem into a number of parallel tasks.
  They are thus well suited to large internet based distributed platforms and do not suffer from parallel slowdown.
  They require little or no communication of results between tasks.

:Distributed computing problems:
  require communication between taks, especially communication of intermediate results.

:Inheritably serial computing problems:
  cannot be parallelized at all. They are diametric opposite to embarrassingly parallel problems.

More General Speedup Formula
----------------------------

A better version of the `Amdahl's law`_

.. math::
   
   \Psi(n,p) \leq \frac{\sigma(n) + \phi(n)}{\sigma(n) + \frac{\phi(n)}{p} + \kappa(n,p)}

Speedup is an increasing function of problem size

Karp-Flatt Metric
-----------------

- analyze parallel program performance
- predict speedup with additional processors

Start with the speedup formula

.. math::

   \Psi(n,p) \leq \frac{\sigma(n) + \phi(n)}{\sigma(n) + \frac{\phi(n)}{p} + \kappa(n,p)}

The experimentally determined serial fraction e is a function of speedup and the number pf processors

.. math::

   e = \frac{1/\Psi - 1/p}{1 - 1/p}

from this we can define :math:`\Psi` in terms of :math:`e` and :math:`p`

.. math::

  \Psi = \frac{p}{e \cdot (p - 1) + 1}

**Interpretation of e**

- if e is constant as num of CPUs increases, then speedup is constrained by the sequential component

Isoefficiency metric
--------------------

- n - data size
- p - num processes
- T(n,p) -- execution time using p processors
- \Psi -- speedup

T_0(n,p) -- the total wasting time spent by processes doing work not done by sequential algorithm
.. math::

   T_0(n,p) = (p - 1) \cdot \sigma(n) + p \cdot \kappa(n,p)

- For example, :math:`T_(n,1)` is the sequential execution time
- We want the algorithm to maintain a constant level of efficiency as the data size n increases


**Main steps to derivation**

- begin with speedup formula
- compute total amount of overhead


.. math::
   T(n,1) \geq C \cdot T_0(n,p)

where 

.. math::

   C = \frac{\varepsilon(n,p)}{1 - \varepsilon(n,p)}


- it is used to determine the max number of CPUs for which 
  the given level of efficiency can be maintained
- How to maintain a given efficiency? --
  To increase the problem size when the number of processors increases
- The maximum problem size we can solve is limited by available amount of memory
- Usually for most parallel systems the memory size :math:`M` 
  is a constant multiple of the number of processors 

Scalability function
~~~~~~~~~~~~~~~~~~~~

- To maintain efficiency :math:`\varepsilon(n,p)` when increasing 
  :math:`p` we must increase :math:`n`
- Max problem size is limited by available memory :math:`M`
- Scalability function :math:`scale(p)` shows how memory usage per processor 
  :math:`M(f(p))` must grow to maintain efficiency
- If the scalability function is constant this means 
  the **parallel system is perfectly scalable**

Examples
~~~~~~~~

:Reduction task:
  collects the answers to all the subproblems and combines 
  them in some way to form the output
:Floyd-Warshall Algorithm:
  graph analysis algorithm for finding shorted path in weighted graph
:Finite difference method:
  numerical methods for approximating the solutions 
  to differential equations using 
  finite difference equations to approximate derivatives

