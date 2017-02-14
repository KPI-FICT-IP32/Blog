=================
Computer networks
=================

:Lecturer: Gabinet Artem Viktorovych

.. contents::
   :depth: 3
..

--------------

Lecture 1. Course overview.
===========================

date: 2016-02-18 08:30:00 +0200

Recommended reading
-------------------

This course is essentially based on `Cisco CCNA
course <https://www.netacad.com/courses/ccna/>`__, hence a lot of things
can be found there.

As for recommended books, you can read the following ones:

-  **Natalia Olifer, Victor Olifer**, *Computer Networks: Principles,
   Technologies and Protocols for Network Design*. This book is
   available on the `publisher’s
   website <http://eu.wiley.com/WileyCDA/WileyTitle/productCd-EHEP000983.html>`__
-  **Andrew Tanenbaum**, *Computer Networks*. This one is available on
   `Amazon <http://www.amazon.com/Computer-Networks-Edition-Andrew-Tanenbaum/dp/0132126958>`__

Course intro
------------

Network components:

-  Devices
-  End devices – devices we use for smth (smartphones, servers, laptops,
   etc)
-  Intermediate devices – devices which allows us to pass data
   (commutators, routers, etc)
-  Medium
-  Messages – pass message from one device to another, big messages are
   splitted to small pieces and being sent separately
-  Rules describe how devices pass messages to each other.

--------------

Lecture 2. Network design. Network models.
==========================================

date: 2016-02-25 08:30:00 +0200

Network design
--------------

There are 4 characteristics of well-designed network. Here they are:

-  **Redundancy**
-  **Scalability** – Network have to be easy to extend witout modifying
   existing parts of the network
-  **QaS (Quality of Service)** – Crucial data must have priority over
   other data
-  **Security**

In the future lectures network topology illustrations will be used.

**Legend:**

    End devices: ``[] Generic, [L] Laptop, [S] Switch``

    Intermediate devices: ``[==] Switch, (+) Router, \(+)/ Wifi router``

When messages are too big, they are split into smaller parts. This is
called **multiplexing**. Packets are enumerated. This allows to restore
a whole message from parts

::

    []--------[==]--(+)
             / |
            /  |
    []-----/   |
               |
               |
     LAN       []

Network types:

-  **LAN** – Local Area Network
-  **WAN** – Wide Area Network
-  **Internet**

Network models
--------------

Standard developers:

-  IEEE Institute of electric and electronics engineering
-  IETF Internet engineering task force

Protocols are described in documents called *RFC*

TCP/IP Model
~~~~~~~~~~~~

+-----+------------------+
| №   | Name             |
+=====+==================+
| 4   | Application      |
+-----+------------------+
| 3   | Transport        |
+-----+------------------+
| 2   | Internet         |
+-----+------------------+
| 1   | Network access   |
+-----+------------------+

OSI Model (developed by ISO)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----+-------------------+
| №   | Name              |
+=====+===================+
| 7   | Application       |
+-----+-------------------+
| 6   | Presentation      |
+-----+-------------------+
| 5   | Session           |
+-----+-------------------+
| 4   | Transport layer   |
+-----+-------------------+
| 3   | Network           |
+-----+-------------------+
| 2   | Data link         |
+-----+-------------------+
| 1   | Physical          |
+-----+-------------------+

-  Application layer is the layer which is used by user applications
-  Presentation layer– data encoding, compressing, etc
-  Session layer – ??
-  Transport layer – transferring data between applications
-  Network layer – transfering data between devices
-  Data link – interface between application and hardware layers
-  Physical layer – hardware level

Each protocol has its own PDU (Protocol data unit).

+------------+-----------+
| Level(s)   | PDU       |
+============+===========+
| 7, 6, 5    | Data      |
+------------+-----------+
| 4          | Segment   |
+------------+-----------+
| 3          | Packet    |
+------------+-----------+
| 2          | Frame     |
+------------+-----------+
| 1          | Bytes     |
+------------+-----------+

--------------

Lecture 3. Physical level.
==========================

date: 2016-03-10 08:30:00 +0200

OSI levels from 2 (Data link) to 7 (application) are software levels.
Developers use them in their software.

The first level (physical) is the trully hardware level.

Physical level generates either electrical/radio/other signals.

Physical level takes incoming frame and encodes it in form of ones an
zeros. Then it generates corresponding signals to send this data.

Physical level responsibilities include:

-  Data encoding/decoding
-  Signaling

Physical level encodings:
-------------------------

NRZ
~~~

::

    NRZ
    |--+   +-----+
    |  |   |     |      
    |  |   |     |      Uses clocking. One bit sent in one bittime (time unit)
    +--+---+-----+-----
      1  0   1  1  0

NRZ was used in really slow connections. There is a problem, when
several same values come in a sequence (like 4 ones), because it is
pretty difficult for receiver to “understand” this data.

Manchester coding (the first one)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    Manchester coding (the first one)
    | +--+   ++ +--+    
    | |  |   || |  |        
    | |  |   || |  |       
    +-+--+---++-+--+------
      1  0   1  1  0

Change from no signal to existing signal is 1 and from existing signal
to no signal is 0. This was much effective than NRZ, but still worked
only for slow connections

4B/5B
~~~~~

Every 4bits are encoded in special combination of 5 bits. That allows
to avoid issues with several same values in sequence.

Disadvantage: data overhead

8B/10B
~~~~~~

The same as 4B/5B, but instead of 4bit and 5bit sequences, 8bit and
10bit are used instead.

Bandwidth
---------

Bandwidth shows how much data can be sent per some time interval.
It is measured in ``bps`` (bits per second)

::

    1000bps  = 1 kbps
    1000kbps = 1 Mbps
    1000Mbps = 1 Gbps
    1000Gbps = 1 Tbps

Bandwidth of Ethernet is 10Mbps

Bandwidth depends on both transmitter and receiver. If transmitter and
receiver have different bandwidth, the lowest of them is used.

::

      1Gbps  10Mbps  1Gbps
    []-----[]------[]-----[]

Bandwidth in above picture is 10Mbps

Throughput and goodput
~~~~~~~~~~~~~~~~~~~~~~

Throughput is the data transmission speed at specific conditions.

::

    max:100Mbps  max:100Mbps
    []------{cloud}-----[]
      60Mbps       100Mbps

Throughput in above picture is 60Mbps

Goodput is the payload transmission speed at specific conditions. That
means, techncal and service data (frame, package, segment, etc) headers
are not counted in goodput.

Connections
-----------

-  Twisted pair
-  Fiber connection
-  Wireless
-  Coaxial

Twisted-pair
~~~~~~~~~~~~

Twisted-pair has two standards:

-  UTP unshielded twisted pair.
-  SPT shielded twisted pair.

Max length of Twisted-pair is 100m

Twisted pair consists of 8 wires.

-  Orange
-  Green
-  Blue
-  Brown

There are 2 standards:

-  T568A
-  T568B

+---+---------+---------+
|   |  T568A  |  T568B  |
+===+=========+=========+
| 1 | Green/  | Orange/ |
+---+---------+---------+
| 2 | Green   | Orange  |
+---+---------+---------+
| 3 | Orange/ | Green/  |
+---+---------+---------+
| 4 | Blue    | Blue    |
+---+---------+---------+
| 5 | Blue/   | Blue/   |
+---+---------+---------+
| 6 | Orange  | Green   |
+---+---------+---------+
| 7 | Brown/  | Brown/  |
+---+---------+---------+
| 8 | Brown   | Brown   |
+---+---------+---------+

| **Straightthrough twisted-pair:** A-A or B-B
| **Crossover twisted-pair:** A-B or B-A

Straighthrough:

-  Switch + PC
-  Switch + Router

Crossover:

-  PC + PC
-  Router + Router
-  Switch + Switch

MDI-x allows us to not bother about which twisted-pair
(Straightthrough or crossover) we use.

Only 4 wires are used to transfer data at 100Mbps. Other 4 are used to
power devices

Fiber
~~~~~

2 types:

-  Multimod (d = 50-60mkn), up to 1.5km
-  Singlemod (d = 9-10mkn), uses laser, up to 80km

--------------

Lecture 4. Fiber. Wireless. Application level.
==============================================

date: 2016-03-17 08:30:00 +0200

Fiber
-----

Fiber cable usually uses two fiber wires: one wire to transmit data in
one direction

There are one-wire fiber cables. These cables use light waves with
different wave length

Two types of connector:

- LC FC
- SC

Ports
~~~~~

-  GBIC - old format
-  SFP (1 Gbps)
-  SFP+ (10 Gbps)
-  QSFP (40Gbps)
-  QSFP+ (80Gbps)

Connection speed can be increased using **link aggregation**: two cables
on the software level recognized as one link, and balancer sends part of
packets on the one cable, and part – on another cable.

Wireless
--------

802.11 standard.

+---------------------+----------------+------------------+
| standard name       | frequency      | speed            |
+=====================+================+==================+
| standard 802.11a    | 2.4Ghz         | up to 11 Mbps    |
+---------------------+----------------+------------------+
| standard 802.11b    | 5Ghz           | up to 52 Mbps    |
+---------------------+----------------+------------------+
| standard 802.11g    | 2.4Ghz         | up to 52 Mbps    |
+---------------------+----------------+------------------+
| standard 802.11n    | 2.4Ghz, 5Ghz   | up to 300 Mbps   |
+---------------------+----------------+------------------+
| standard 802.11ac   | 2.4Ghz, 5Ghz   | > 1 Gbps         |
+---------------------+----------------+------------------+

2.4 Ghz is used by wide variety of devices, hence if there is another
device which works on this frequency nearby, the major loss of quality
will occur due to signal interference.

There are three channels which do not overlap at 2.4Ghz frequency. These
are 1st, 6th and 11th channels.

Application level
-----------------

Main protocols:

-  HTTP
-  DNS
-  DHCP
-  FTP
-  telnet
-  SSH
-  IMAP
-  POP3
-  SMTP

| Client/Server architecture
| Peer-to-peer (P2P)

FTP
~~~

Data transfered in a plain form. No encryption.

DHCP
~~~~

Dynamic host configuration protocol.

#. Client broadcasts request to receive IP address (DHCP-discover)
#. DHCP server finds accessible ip addresses and returns DHCP-offer.
#. Client receives DHCP-offer and broadcasts its intent to use offer.
   (DHCP-Request)
#. Corresponding DHCP server registers client and returns
   DHCP-Acknowledge response to client
#. Client saves received IP address

--------------


Lecture 5. Application level protocols. Telnet. SSH. HTTP. DNS.
===============================================================

date: 2016-03-24 08:30:00 +0200

Common protocols
----------------

DHCP, FTP are text protocols

Telnet
~~~~~~

| Was developed for remote access to other device’s console.
| Uses client-server architecture

All logins, passwords data are passed in unencrypted way.

SSH
~~~

Secure SHell

| Was developed for remote access to other device’s console.
| Uses client-server architecture

All logins, passwords data are passed encrypted.

HTTP
~~~~

HyperText Transfer Protocol

Client-server architecture

::

    Client  Webserver
      [L]-------[S]

| HTTP protocol up to version 1.1 (inclusive) is text protocol.
| HTTP 2.0 is binary

HTTP request according to protocol consists of 3 parts

-  | Request string (mandatory)
   | Request string consists of

   +-------------------------------+------------------------+--------------------+
   | Request type                  | Resource identifier    | Protocol version   |
   +===============================+========================+====================+
   | GET/POST/PUT/PATCH/DELETE/…   | in general it is URI   | i.e HTTP/1.1       |
   +-------------------------------+------------------------+--------------------+

   Example request string: ``GET http://google.com.ua/ HTTP/1.1``

-  Request headers (optional)
-  message body (optional)

| HTTP protocol is stateless. Hence workaround is required to store
  state. Such workaround is called ``Cookies``.
| Cookies are passed as request headers. Usually they are encoded in
  base64

DNS
~~~

Domain Name Service

This protocol is used to resolve request url into actual IP address.

Domain name system is a distributed structure.
On the top of this structure root domain-name server is placed. This
one knows how to resolve top level of domain name.
On the next level first-level domain servers are placed. They “know”
where to find second-level domain servers and so on and so forth.

::

                       [root (.)]
              +------+----+---+------+-----+
            [com]   [ua]    [edu]  [org]  [io] ...
           +--+--+
           |     |
         [vk]   [github]...

Fully qualified domain name ends with dot: ``fiot.kpi.ua.``

Domain name is resolved from end to beginning. DNS server delegates
request to the corresponding lower-level DNS server.

If we want to open ``mlp.wikia.com``:

#. DNS resolution request to DNS server to associate domain name with IP address.

   #. request [.] for ``mlp.wikia.com``. response [com] DNS server
   #. request [com] for ``mlp.wikia.com``. response [wikia.com] DNS server
   #. request [wikia.com] for ``mlp.wikia.com``. response [mlp.wikia.com] IP address

Types of DNS records:
>>>>>>>>>>>>>>>>>>>>>

-  A. Domain name is associated with IP:
   ``foto IN A 77.77.77.77``
-  | PTR associates IP address with domain name. **in-addrarpa**.
   | (77.47.128.130)

   ::

           in-addrarpa
            |  .... \ ...
           77
            |
           47
            |
           128
            |
           130

-  TXT.
-  SOA. (Self-off authority). Describes DNS server responsibilities
   (authority)
-  NS. name server.
   ``kpi.ua IN NS ...``
-  MX (Mail eXchange).

DNS lookup can be either interactive (DNS Server delegates to another
DNS server) or recursive (Server recursively searches for response
without delegating)

.. note::

  ``nslookup`` tool =)

Mail Protocols:
---------------

::

          SMTP           IMAP/POP3
     [L]------------[S]-------------[PC]
     sender      mail server       receiver

IMAP
~~~~

| This one is used to receive emails. This protocol is newer than POP3.
| IMAP loads only mail headers. And concrette message will be loaded as
  requested.

POP3
~~~~

This one is used to receive emails. It loads whole email messages at
once.

SMTP
~~~~

This protocol is used to send email.

--------------

Lecture 6. Transport layer.
===========================

date: 2016-03-31 08:30:00 +0200

Transport level
---------------

PDU: Segment

-  **data exchange between applications**. It does not matter, where the
   application is, it only matters which application. So transport level
   does not transmits data between hosts, it only determines which data
   belongs to which application and passes data from/to corresponding
   application.
-  splits data into small parts (chunks)
-  determines, which application received data belongs to
-  message tracking
-  flow controll.

Message passing on transport level
----------------------------------

#. Ordering received messages
#. Reliability. Wait for transmission confirmation.
#. Flow controll. Message will be transfered in batches (several parts
   transmitted at a time)
#. Segmentation.

Protocols
---------

| Dependeing on protocol specific header is added to message.
| In both TCP and UDP application identifier is passed in header. 2b is
  used to store this application id. Hence there are 2^16 unique
  identifiers **(ports)**.

| Ports from 0 to 1023 are called *well-known*
| Ports from 1024 to 49151 are called *registered ports*. Use these
  ports when you develop your app
| Ports from 49152 to 65535 are *Dynamic* ports

+------------+---------+--------------------------------------------------------------+
| Protocol   | Port    | Transfer protocol                                            |
+============+=========+==============================================================+
| FTP        | 20,21   | TCP                                                          |
+------------+---------+--------------------------------------------------------------+
| SSH        | 22      | TCP                                                          |
+------------+---------+--------------------------------------------------------------+
| TELNET     | 23      | TCP                                                          |
+------------+---------+--------------------------------------------------------------+
| SMTP       | 25      | TCP                                                          |
+------------+---------+--------------------------------------------------------------+
| DNS        | 53      | UDP (when client requests data), TCP (to sync DNS servers)   |
+------------+---------+--------------------------------------------------------------+
| DHCP       | 67,68   | UDP                                                          |
+------------+---------+--------------------------------------------------------------+
| HTTP       | 80      | TCP                                                          |
+------------+---------+--------------------------------------------------------------+
| POP3       | 110     | TCP                                                          |
+------------+---------+--------------------------------------------------------------+
| IMAP       | 143     | TCP                                                          |
+------------+---------+--------------------------------------------------------------+

Within header both source and destination ports are passed.

::

     SRC PORT   DST PORT       DATA 
    +---------+----------+-------------+
    |  50000  |    80    |             |
    +---------+----------+-------------+

TCP. Transmission controll protocol
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  TCP protocol **guarantees** data transmission.
-  Header size: 20b

::

    |16b   SRC PORT|16b   DST PORT|
    |6b:flags|                    |
    |32b: ISN                     |

-  Before data transmission source and destination establish TCP
   connection (3-wave handshake):

::

    |                      |
    |------SYN,seqa------->|
    |                      |
    |<---SYN,ACK(seqb)-----| If there is nothing on this port RST returned instead
    |                      |
    |----ACK(seqb + 1)---->| Now we have TCP connection established
    |                      |
    |                      |
    |                      |
    |---DATA(1602)-------->| Data size passed within seq param. 1602 is size here
    |                      |
    |<---ACK(1603)---------| Data transfer ackknowledge.
    |                      |
    |                      |
    |-----FIN------------->| A sent all data and wants to finish connection
    |<----FIN--------------| B wants to finish connection too
    |-----ACK------------->| Confirm connection end
    A                      B

flags: SYN, ACK, RST, FIN, PUSH, URG

-  TCP tries to send more data with every sequential request. I.E.
   within first transfer it sends 1kb. Then 2, 4,8,16 and so on and so
   forth. (flow control)

   use ``netstat``

UDP. User datagram protocol.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Does **NOT** guarantee data transmission
-  Header size: 8b

--------------

Lecture 7. Network layer. IPv4
==============================

date: 2016-04-07 08:30:00 +0200

Network layer
-------------

In addition to data encapsulation and decapsulation which occur on every
layer, network layer is also responsible for addressing devices and
routing.

Network layer protocols include

-  IPv4
-  IPv6

Network layer is fully unreliable. You cannot be sure if the data will
be sent/received.

Network layer protocols are unaware of data transmission method (wifi,
ethernet, smth else) used at physical layer.

Nets and subnets
----------------

::

        [ ]-  -[ ]
            \/
     [ ]----------[ ]
            /\
        [ ]-  -[ ]

    This how it used to be earlier

| But now there are so many devices that having one net for all of them
  is not enough.
| Here subnets are coming for rescue.

There are different ways of distributing subnets (or splitting net into
subnets)

-  **geographical.** This is the dummiest way. I.E. one floor in
   10-floor building has its own subnet.
-  **purpose.** Some people (finance dpt) need high reliable conection
   for work and other (managers) does not. We can create subnets for
   every group of peopple with specia configuration
-  **security.** Sometimes for security reasons we need to restrict
   access for different groups of devices. Subnets for the rescue.

::


       [ ]-              -[ ]
           \            /
     [ ]---[=]---(+)---[=]---[ ]
           /            \
       [ ]-              -[ ]

    Now we have two subnets =)

Gateway is used to communicate between subnets.

Addressing
~~~~~~~~~~

Sample IPv4 address: ``193.47.196.75``. IPv4 address’ length is 32bits
(4 octets). It consists of 4 bytes splitted with dots.

IP address consists of two parts:

-  Network part
-  Host part

::

    193.47.196.75  /24
    ----------|----|----
    Network   |Host|Prefix
    part      |part|

| Prefix determines how many bits are used for network part
| To determine IP address of network we have to fill host part of IP
  address with zeros.
| To get broadcast address we have to fill host part of IP address with
  ones. (bits)

+----------------+---------------------+
| Address type   | IP address          |
+================+=====================+
| Host IP        | 192.47.196.75/24    |
+----------------+---------------------+
| Network IP     | 192.47.196.0/24     |
+----------------+---------------------+
| Broadcast IP   | 192.47.196.255/24   |
+----------------+---------------------+

Number of available hosts in network is:

$$ N = 2^n - 2 $$

Here

-  $N$ is the number of available hosts in network
-  $n$ is the length of the host part in bits $$n = 32 - prefix$$

IPv4 address classification:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    | Class | IP address range           |Prefix| Note                           |
    |-------|----------------------------|------|--------------------------------|
    |   A   |  1.0.0.0 -- 127.255.255.255| /8   | These networks were given to   |
    |   B   |128.0.0.0 -- 191.255.255.255| /16  | big organizations as there are |
    |   C   |192.0.0.0 -- 223.255.255.255| /24  | a lot of available hosts       |
    |-------|----------------------------|------|--------------------------------|
    |   D   |224.0.0.0 -- 239.255.255.255|      | Multicast addresses            |
    |   E   |240.0.0.0 -- 255.255.255.255|      | Reserved addresses             |

There are some reserved addresses:

-  127.0.0.0/8 – localhost
-  169.254.0.0/16 – M$ addresses used in networks w/o DHCP
-  192.0.52.0/24 – WTF is this?
-  0.0.0.0
-  255.255.255.255 – network broadcast address

Addresses can be either public or private. Private addresses are used in
private networks and are unaccessible from Internet.

Private addresses lay in the following ranges:

-  10.0.0.0/8
-  172.16.0.0/12 – 172.31.255.255/12
-  192.168.0.0/16

NAT
~~~

| NAT stands for Network address translation. This topic will be covered
  after test will be passed.
| This is used to give Internet access for devices which obtain private
  IPv4 address

Message types:
~~~~~~~~~~~~~~

There are three *main* types of messages:

#. **Unicast**. Only one host is the recipient of mesage.
#. **Broadcast**. Message is sent to every available host in the
   broadcast domain. One broadcast domain is equal to one subnet.
   Broadcast messages do not pass through layer-3 devices.
#. **Multicast**. Multicast messages are sent to specified group of
   devices.
#. **Anycast**. Messages are routed to the topologically nearest node in
   a group of potential receivers, though it may be sent to several
   nodes, all identified by the same destination address.
#. **Geocast**. Message is sent to a group of destinations in a network
   identified by their geographical locations. It is a specialized form
   of multicast addressing used by some routing protocols for mobile ad
   hoc networks.

--------------

Lecture 8. Subnets. Test preparations.
======================================

date: 2016-04-14 08:30:00 +0200

Subnets
-------

IANA organization is responsible for distributing IPv4 addresses. It
used to be a single organization, but nowadays it has transformed into
group of organizations:

-  ARIN (North America)
-  APNIC (Asia)
-  AFRINIC (Africa)
-  RIPENCC (Europe)
-  ACNIC (Australia))

Splitting network into subnets:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Given: ``193.175.16.0 / 24``

In binary format: ``11000001.10101111.000100000.00000000 / 24``

Assume, we want to make $$n = 2$$ subnets:

Increase network part by $$\\lceil log \_{2}(n) \\rceil = 1$$ :
``11000001.10101111.000100000.0 | 0000000 / 25``

Now we can have 2 subnets. Here they are:

-  ``11000001.10101111.000100000.0 | 0000000 / 25``
-  ``11000001.10101111.000100000.1 | 0000000 / 25``

Rewrite addresses in decimal:

-  ``193.175.16.0 / 25``
-  ``193.175.16.128 / 25``

Assume, we want to split ``193.175.16.128 / 25`` into $$n = 4$$ subnets:

Increase network part by $$ \\lceil log \_{2}(n) \\rceil = 2 $$ :
``11000001.10101111.000100000.100|00000 / 27``

Now we can have 4 subnets. Here they are:

-  ``11000001.10101111.000100000.100 | 00000 / 27``
-  ``11000001.10101111.000100000.101 | 00000 / 27``
-  ``11000001.10101111.000100000.110 | 00000 / 27``
-  ``11000001.10101111.000100000.111 | 00000 / 27``

Rewrite addresses in decimal:

-  ``193.175.16.128 / 27``
-  ``193.175.16.160 / 27``
-  ``193.175.16.192 / 27``
-  ``193.175.16.224 / 27``

Planning network
~~~~~~~~~~~~~~~~

Given:

-  193.175.16.0 / 24
-  Five departments:

   +-------+-------+----------+-----------+
   | DPT   | PCS   | prefix   | network   |
   +=======+=======+==========+===========+
   | A     | 27    |          |           |
   +-------+-------+----------+-----------+
   | B     | 100   |          |           |
   +-------+-------+----------+-----------+
   | C     | 15    |          |           |
   +-------+-------+----------+-----------+
   | D     | 4     |          |           |
   +-------+-------+----------+-----------+
   | E     | 30    |          |           |
   +-------+-------+----------+-----------+

#. Determine subnet prefixes according to number of PCs:

   +-------+-------+----------+-----------+
   | DPT   | PCS   | prefix   | network   |
   +=======+=======+==========+===========+
   | A     | 27    | /27      |           |
   +-------+-------+----------+-----------+
   | B     | 100   | /25      |           |
   +-------+-------+----------+-----------+
   | C     | 15    | /27      |           |
   +-------+-------+----------+-----------+
   | D     | 4     | /29      |           |
   +-------+-------+----------+-----------+
   | E     | 30    | /29      |           |
   +-------+-------+----------+-----------+

       **TODO:** *Describe this process*

#. Split network into subnets:

       **TODO:** *Describe this process*

#. Assign subnets to department

       **TODO:** *Describe this process*

Test preparations
-----------------

Task 1
~~~~~~

Task Description
>>>>>>>>>>>>>>>>

**Given:** ``177.250.13.246 / 28``

**Find:** Network, Netmask, Broadcast address, 1st and last host IP in
network:

Solution
>>>>>>>>

#. Write down IP in binary form:
   ``101110001.11111010.00001011.11110110``
#. Determine host and network parts:
   ``101110001.11111010.00001011.1111 | 0110``
#. Net: fill host part with zeros:
   ``101110001.11111010.00001011.1111 | 0000``
#. Netmask: fill network part with ones and host part with zeros:
   ``111111111.11111111.11111111.1111 | 0110``
#. Broadcast: fill host part with ones:
   ``101110001.11111010.00001011.1111 | 1111``
#. First available IP: ``101110001.11111010.00001011.1111 | 0001``
#. Last available IP: ``101110001.11111010.00001011.1111 | 1110``

Finally transform binary results to decimal:

#. Net: ``177.250.13.240``
#. Netmask: ``255.255.255.240``
#. Broadcast: ``177.250.13.255``
#. First available IP: ``177.250.13.241``
#. Last available IP: ``177.250.13.254``
#. Total IP addresses available: $$ 2 ^ {32 - 28} - 2 = 14 $$

Task 2. Split network into subnets.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    **NOTE:** I’m not sure, I got it right. Please correct me if I made
    a mistake, otherwise remove this note if you can.

Task Description
>>>>>>>>>>>>>>>>

**Given:**

-  ``10.1.14.0 / 24``
-  departments:

   +-------+-------+----------+----------+
   | dpt   | PCs   | prefix   | subnet   |
   +=======+=======+==========+==========+
   | 1     | 13    |          |          |
   +-------+-------+----------+----------+
   | 2     | 120   |          |          |
   +-------+-------+----------+----------+
   | 3     | 15    |          |          |
   +-------+-------+----------+----------+
   | 4     | 61    |          |          |
   +-------+-------+----------+----------+
   | 5     | 2     |          |          |
   +-------+-------+----------+----------+

**To do:** Divide to subnets and assign subnets.

Solution
>>>>>>>>

#. Determine prefixes. I.E. For 120:

   -  Keep in mind that you have to add 2 to number of PCs, as one
      address will be used as network address and other one will be used
      for broadcast.
   -  Nearest bigger power of two is 128.
   -  Thus we need $$ log \_{2}(128) = 7 $$ bits for the host part
   -  And finally calculate the network prefix: $$ prefix = 32 - 7 = 25
      $$

   +-------+-------+----------+----------+
   | dpt   | PCs   | prefix   | subnet   |
   +=======+=======+==========+==========+
   | 1     | 13    | /28      |          |
   +-------+-------+----------+----------+
   | 2     | 120   | /25      |          |
   +-------+-------+----------+----------+
   | 3     | 15    | /28      |          |
   +-------+-------+----------+----------+
   | 4     | 61    | /26      |          |
   +-------+-------+----------+----------+
   | 5     | 2     | /30      |          |
   +-------+-------+----------+----------+

#. Divide net into subnets:

   -  10.1.14.0 / 25
   -  10.1.14.128 / 25

      -  10.1.14.128 / 26
      -  10.1.14.192 / 26

         -  10.1.14.192 / 28
         -  10.1.14.208 / 28
         -  10.1.14.224 / 28
         -  10.1.14.240 / 28

            -  10.1.14.240 / 30
            -  10.1.14.244 / 30
            -  10.1.14.248 / 30
            -  10.1.14.252 / 30

#. Assign subnets:

   +-------+-------+----------+--------------------+
   | dpt   | PCs   | prefix   | subnet             |
   +=======+=======+==========+====================+
   | 1     | 13    | /28      | 10.1.14.192 / 28   |
   +-------+-------+----------+--------------------+
   | 2     | 120   | /25      | 10.1.14.0 / 25     |
   +-------+-------+----------+--------------------+
   | 3     | 15    | /28      | 10.1.14.208 / 28   |
   +-------+-------+----------+--------------------+
   | 4     | 61    | /26      | 10.1.14.128 / 26   |
   +-------+-------+----------+--------------------+
   | 5     | 2     | /31      | 10.1.14.240 / 30   |
   +-------+-------+----------+--------------------+

--------------

Lecture 9. Routing
==================
date: 2016-04-28 08:30:00 +0200

| One of the Network Layer responsibilities is routing.
| Among the data, which is sent, destination IP and source IP are passed
  over network. This is done to make possible determine sender and
  reciever. Transport protocol code is also passed in package headers.
  To make sure that header is OK, CRC checksum is passed in that header
  (recursion, yup)

ICMP protocol
-------------

Internet control message protocol. This protocol is used for network
diagnostics. It works over the Network layer. One of the most well-known
features of thisprotocol is ability to check node availability.

| TTL – time to live
| Every 3rd level device (like router) decrease TTL by one. If TTL value
  is 0, then device drops the packet. Initial TTL value is set by
  sender. That depends on OS.

RTT – Round trip time

::

    []---[==]-(+)---(+)---(+)---[]

Routing
-------

WTF is router? (+)
~~~~~~~~~~~~~~~~~~

    Router is a box with holes, buttons, wires and light indicators. It
    is some sort of computer, without monitor. There are CPU, RAM, NVRM,
    ROM, physical interfaces, etc…

Router is a 3rd level device. That means, it works on 3rd (Network)
layer.

Despite everything else router allows us to unite different networks
with each other, find best path to some host, and so on and so forth.

Routing table
~~~~~~~~~~~~~

Every router stores routing table. Routing table stores records of
networks, next-hop or interfaces, where the network is.

There are 3 types of records in routing table:

#. **Directly connected.** It appears as soon as router is enabled or
   device is plugged into network/router
#. **Static routes.** System administrators/users fill these records.
#. **Dynamic routes.** These records are populated by routers
   themselves, depending on their configurations.

Rules of routing
~~~~~~~~~~~~~~~~

#. If you have a route on one router in netwrok, it does not mean other
   ruoters have that route.
#. If you create a route, you have to create a backward one
#. Next-hop **must** be in directly-connected network

Static routes
~~~~~~~~~~~~~

.. warning::

    I’ve messed upo this topology. PLS FIX IT!

::

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


**R1**

| 192.168.1.0/24 \| i1
| 192.168.4.0/30 \| i2
| 192.168.3.0/24 \| 192.168.4.2

192.168.3.0/24 next-hop 192.168.4.1

**R2**

| 192.168.4.0/30 \| i1
| .2.0/24 \| i3
| .5.0/30 \|
| .3.0/24 \| 192.168.5.2

--------------

Lecture 10. Dynamic routing
===========================

date: 2016-05-12 08:30:00 +0200

::

                    R2
                ----(+)-| B
          R1   /     |
    A |---(+)--      |
               \     |
                ----(+)-| C
                    R3

There are some running processes on routers. They exchange some data,
which allow to build routing tables for networks.

Chief weaponry of dynamic routing protocols include such diverse things
as

-  Messages
-  Path finding algorithms
-  Corresponding data structures

Comparisson of static and dynamic routing
-----------------------------------------

+-------------------+-------------------------------------------------------+---------------------------------------+
| Criteria          | Static                                                | Dynamic                               |
+===================+=======================================================+=======================================+
| Scaleability      | Bad: network must be reconfigured manually to scale   | **Good**                              |
+-------------------+-------------------------------------------------------+---------------------------------------+
| Knowledges        | **Little knowledge**                                  | A lot of knowledge required           |
+-------------------+-------------------------------------------------------+---------------------------------------+
| CPU, resourses    | **Minimal**                                           | Uses CPU to configure routing         |
+-------------------+-------------------------------------------------------+---------------------------------------+
| Reconfiguration   | Complex                                               | **Simple**                            |
+-------------------+-------------------------------------------------------+---------------------------------------+
| Security          | **Good**                                              | Bad                                   |
+-------------------+-------------------------------------------------------+---------------------------------------+
| Fault tolerance   | Extremely bad                                         | **Good (depends on used protocol)**   |
+-------------------+-------------------------------------------------------+---------------------------------------+

Routing configuration protocols can be divided into two groups:

-  **IGP** Interior gateway protocol
-  **EGP** Exterior gateway protocol

**Autonomic system** is a group of networks running under a single
administrative control. This could be our company or a branch of
company. Just like Subnetting AS is also used to break a large network
in smaller networks.

Classification
--------------

-  EGP
-  `BGP <https://en.wikipedia.org/wiki/Border_Gateway_Protocol>`__
-  IGP
-  distance-vector

   -  `RIP <https://en.wikipedia.org/wiki/Routing_Information_Protocol>`__
   -  `IGRP <https://en.wikipedia.org/wiki/Interior_Gateway_Routing_Protocol>`__
   -  `EIGRP <https://en.wikipedia.org/wiki/Enhanced_Interior_Gateway_Routing_Protocol>`__

-  link-state

   -  `IS-IS <https://en.wikipedia.org/wiki/IS-IS>`__ (Intermediate
      system to intermediate system)
   -  `OSPF <https://en.wikipedia.org/wiki/Open_Shortest_Path_First>`__
      (Open shortest path first)

Distance-vector protocol know nothing but the next hop and some metric,
called distance.

Link-state protocols try to build a full network topology graph and then
find paths on that graph.

RIP =(
------

::

      A   R1   B  R2   C  R3   D
    |-----(+)-----(+)-----(+)-----|

+---------------+---------------+---------------+
| R1            | R2            | R3            |
+===============+===============+===============+
| A - 0         | B - 0         | C - 0         |
+---------------+---------------+---------------+
| B - 0         | C - 0         | D - 0         |
+---------------+---------------+---------------+
| ———–          | ———–          | ————          |
+---------------+---------------+---------------+
| *C: R2 - 1*   | *D: R3 - 1*   | *B: R2 - 1*   |
+---------------+---------------+---------------+
|               | *A: R1 - 1*   |               |
+---------------+---------------+---------------+

Every 30 seconds routers broadcast their routing table to their
“neighbours”.

Metrics:

+---------------+------------+
| Metric        | Protocol   |
+===============+============+
| - Hop count   | RIP        |
+---------------+------------+
| - Bandwidth   |            |
| - Delay       |            |
| - Load        | EIGRP      |
| - Reliability |            |
+---------------+------------+
| - Cost        | OSPF       |
+---------------+------------+

If there are several paths with the same metrics, RIP (as well as any
other protocol) will balance traffic among these pathts.

Maximum diameter of network, to which RIP can be applied is **15**

**Split horizont**. If router R2 received path to D from R3, it will not
send recieved path (D) to R3.

--------------

Lecture 12. Cool stuff
======================

date: 2016-05-12 08:30:00 +0200

DHCP
----

::

            [ ] DHCP
             |
             |
           [===]----------(+)----{ INTERNET }
           / | \
          /  |  \
       [ ]  [ ]  [ ]

| As we know, DHCP requests do not pass through third-layer devices.
| But what if we have a topology like this?

::

               DHCP  [ ]---[===]---[ ] WEB
                             / 
                            /
           [===]---------1(+)----{ INTERNET }
           / | \            2 
          /  |  \            \
       [ ]  [ ]  [ ]        [===]
                            / | \
                           /  |  \
                        [ ]  [ ]  [ ]

To handle this we could use own DHCP server for each subnetwork, which
is extremely inconvenient and expensive (A lot of subnets == A lot of
expensive server hardware). How can we handle this?

-  Setup **DHCP Relay** on router ports 1 and 2!!!
-  Setup default gateway for router

Now the router will repack BROADCAST DHCP requests into UNICAST requests
and pass them to DHCP server.

-  Setup IP pools for DHCP server:

.. code:: json

    { 
        "pool1": {
            "for network": "192.168.1.0/24",
            "def gateway": "192.168.1.254",
            ...
        },
        "pool2": {
            "for network": "192.168.2.0/24",
            "def gateway": "192.168.2.254",
            ...
        },
        ...
    }

And voila! If you did everything correctly, your DHCP server will serve
to several subnets as well as it does to one!

    If your DHCP server goes down, your whole network goes down. To
    handle this you may want to configure **DHCP Failover**

NAT
---

IPv4 has too little IP addresses to assign to devices. There are even
much less public addresses. However there are a lot of devices, which
need to have an IP address. So how can we workaround this?

::

            [ ] DHCP
             |
             |              77.47.10.1
           [===]------.254(+)------------{ INTERNET }
           / | \                              |
         .1  .2 .3                          [   ] WEB
       [ ]  [ ]  [ ]                          vk.com (1.1.1.1)

       192.168.1.0/24

NAT stands for Network Address Translation. There are 3 Types of NAT:

-  Static
-  Dynamic
-  Masquarade

Static NAT
~~~~~~~~~~

If router recieves request to Internet from 192.168.1.1 then it
translates address to 77.47.11.1 We’ll have the following header:

+--------------+-----------+--------+
| Source       | Dest      | Data   |
+==============+===========+========+
| 77.47.11.1   | 1.1.1.1   | Data   |
+--------------+-----------+--------+

When router recieves request from outer (like 1.1.1.1) to 77.47.11.1 it
translates destination IP to corresponding Internal address
(192.168.1.1)

All translations are saved in NAT table.

Static NAT is not really good, because it requires to have public
address for each device.

Dynamic NAT
~~~~~~~~~~~

Instead of setting correspondence between addresses it sets
correspondence between pools of addresses and public address. If several
requests from pool are received, they are translated in sequential
order.

Masquarade NAT (PAT)
~~~~~~~~~~~~~~~~~~~~

**PAT** stands for Port Address Translation.

| All requests from (i.e. .254) port of router are translated into one
  public IP address.
| I.E. we are sending request from .1 PC:

+------+-------------+---------+
|      | SRC         | DST     |
+======+=============+=========+
| IP   | 192.168.1.1 | 1.1.1.1 |
+------+-------------+---------+
| Port | 33101       | 80      |
+------+-------------+---------+

Then we’ll have the following record in NAT table:

+---------------+--------------+--------------+---------------+-----------+------------+
| Local IP      | Local Port   | Global IP    | Global Port   | DST IP    | DST Port   |
+===============+==============+==============+===============+===========+============+
| 192.168.1.1   | 33101        | 77.47.10.1   | 20001         | 1.1.1.1   | 80         |
+---------------+--------------+--------------+---------------+-----------+------------+

If router will recieve another request (even to the same resource) from
192.168.1.2 during request it’ll add another record to NAT table and
perform a corresponding substitute

+---------------+--------------+--------------+---------------+-----------+------------+
| Local IP      | Local Port   | Global IP    | Global Port   | DST IP    | DST Port   |
+===============+==============+==============+===============+===========+============+
| 192.168.1.1   | 33101        | 77.47.10.1   | 20001         | 1.1.1.1   | 80         |
+---------------+--------------+--------------+---------------+-----------+------------+
| 192.168.1.2   | 54104        | 77.47.10.1   | 20002         | 1.1.1.1   | 80         |
+---------------+--------------+--------------+---------------+-----------+------------+

When response is recieved, corresponding record will be deleted from
table.

    What happens inside NAT stays inside NAT. No internal activity is
    visible from outside.

But what if we **need** to access some internal resource from outside?
**Port Forwarding** is used for that. You configure NAT so it translates
all incoming requests to specific port (i.e. 8080) to specific device
(i.e. 192.168.1.3)

Firewall
--------

Firewall is used to filter requests according to some rules. I.E. you
may drop all requests to 8080 port both incoming and outcoming.

Interestings
------------

You can use `Wireshark <https://www.wireshark.org/>`__ to discover and
explore your network traffic. This application allows you to analyse
incoming and outcoming packages. Have fun =)
