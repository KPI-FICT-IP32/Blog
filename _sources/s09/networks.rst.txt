====================
Network technologies
====================

:Lecturer: `Rokovyi Oleksandr Petrovych <http://comsys.kpi.ua/ukrainian/teachers/57/>`_

.. contents::
   :depth: 3

--------------

UNIX and Linux systems
======================

.. note::

    further *UNIX/Linux* denotes all Linux, UNIX, Linux-like and UNIX-like
    systems

- There are two types of resources: **files** and **processes**. However file
  entity is much wider than one in Windows systems. Hardware devices, IPC
  mechanisms, etc are represented as files. There are 6 types of files:

  - **Regular file**
  - **Directory**
  - **Device** These are so called *interface files* for real devices. They do
    not store used data but provide an interface for operating system to work
    with underlying hardware devices.

    - **Block device** (data storages like HDD or SDD). Data exchange with such
      devices is done in chunks called blocks. In case of HDDs and SDDs size of
      block is 512B.
    - **Char device**. These devices are mostly used for I/O. System reads and
      writes data to char devices byte by byte.
  - **Socket** allows to exchange data between processes which are run on
    different physical devices. Sockets can be used for IPC on local machine but
    this is not efficient due to network stack it uses.
  - **Pipe** (IPC mechanism). In order to perform some data exchange between
    processes pipes are used. One process opens pipe for reading and other one
    for writing.

        This is like socket but the processes are run on the same physical node

        --- © `Roman Statkevych <https://github.com/IcedNecro>`_

  - **Link**

    - **Hardlink** is a one-way link between filename and its metadata in the
      inode. This means that filename knows where the metadata is but metadata
      knows nothing about filename.

      However metadata is aware about the number of file names which point to
      it.

      *Hardlinks work only within the same filesystem and can be applied only
      for regular files*

    - **Symlink** is a file which contains the path to other file. Symlinks do
      not work with file metadata and they can work among different filesystems
      as well as they can work with directories.

  This allows to manage everything in one way: by changing permissions on the
  filesystem level.

  .. note::

     further the word *file* denotes file of any of 6 types

- Filesystem hierarcy is important. It is represented as a tree, which starts
  from root (``/``). The mechanism behind the hierarcy is simple directories.
  Pay attention that directories do not store user data, but only a list of
  files which are located in that directory.

  There is a filesystem struture standard which defines where the parts of
  operating system are located, where which kinds of files are located, etc.

There are two ways to reference files in UNIX/Linux systems:

- *absolute* filepaths (those are started with ``/`` like ``/home/username``)
- *relative* filepaths (``username/foo/bar``)

.. note::

   In order to get help on any command system manual pages should be used.
   There is a special command ``man`` for that. Details on this command usage is
   available on the `man page for man command
   <https://linux.die.net/man/1/man>`_

Main utility to navigate filesystems is ``cd`` command, reference for which can
be found in `man 1 cd <https://linux.die.net/man/1/cd>`_. Here are some
examples:

.. code-block:: bash

   cd /home/user  # navigate to `/home/user` directory
   cd user  # navigate to directory `user` which is located in current directory
   cd ./user  # the same as above, `.` denotes current directory
   cd ../  # navigate one level up in the directory tree
   cd ../mydir  # navigate to the directory mydir which is on the same level as
   # current dir
   cd ~  # navigate to the current user's home directory
   cd ~/foo # navigate to the directory `foo` which is the home directory

There are other useful utilities:

- `cp <https://linux.die.net/man/1/cp>`_ -- copies files
- `rm <https://linux.die.net/man/1/rm>`_ -- deletes (removes) files
- `touch <https://linux.die.net/man/1/touch>`_ -- create empty file (actually
  change file timestamps)
- `pwd <https://linux.die.net/man/1/pwd>`_ print working directory
- `ls <https://linux.die.net/man/1/ls>`_ list files
- `mv <https://linux.die.net/man/1/mv>`_ move files
- `find <https://linux.die.net/man/1/find>`_ search for files in directory tree

Filesystem hierarcy standard
----------------------------

.. note::

   See ``man hier`` for more details

- ``/``

  - ``boot/`` -- stores boot files. It usually contains kernel, initramfs image,
    bootloader cofiguration files, etc
  - ``etc/`` -- stores configuration files for both operating system and
    applications.
  - ``bin/`` -- stores executable files (which have the highest important for
    operating system).
  - ``sbin/`` -- like ``/bin`` holds less important executables for operating
    system start.
  - ``lib/`` -- holds shared libraries that are necessary to boot the system and
    to run the commands in the root filesystem.
  - ``root/`` -- home directory for ``root`` user
  - ``usr/`` -- (UNIX System resources) holds all other resources, which are not
    included in other directories

    - ``bin/`` -- primary directory for executable programs
  - ``var/`` -- holds temporary operating system files like logs, pid files and
    temporary sockets.
  - ``tmp/`` -- holds *user* temporary data
  - ``mnt/`` -- mountpoints
  - ``home/`` -- holds home directories for users
  - ``media/`` -- mountpoints for external storages like usb sticks
  - ``opt/`` -- additional appliations are installed here
  - ``srv/`` -- storing network services files
  - ``proc/`` -- virtual filesystem which holds info about running processes
  - ``sys/`` -- virtual filesystem which grants access to system
  - ``dev/`` -- stores device files for hardware devices

Permission management
---------------------

There are three subjects for which permissions are set in UNIX/Linux systems for
every file:

- ``u`` -- owner user
- ``g`` -- owner group
- ``o`` -- other users

Main permissions are

- ``r`` -- read permission
- ``w`` -- write permission
- ``x`` -- execute permission

.. code-block:: bash

   $ ls -l
   total 73
   -r--r--r--   1 root  wheel  6199 Jul 21 02:11 COPYRIGHT
   drwxr-xr-x   2 root  wheel  1024 Jul 21 02:09 bin
   drwxr-xr-x   8 root  wheel  1536 Sep 13 02:39 boot
   dr-xr-xr-x  12 root  wheel   512 Sep 13 02:39 dev
   -rw-------   1 root  wheel  4096 Sep 13 02:40 entropy
   drwxr-xr-x  27 root  wheel  2560 Sep 13 02:57 etc
   lrwxr-xr-x   1 root  wheel     8 Sep 13 02:05 home -> usr/home
   drwxr-xr-x   4 root  wheel  1536 Jul 21 02:09 lib
   drwxr-xr-x   3 root  wheel   512 Sep 13 02:03 libexec
   drwxr-xr-x   2 root  wheel   512 Jul 21 02:08 media
   drwxr-xr-x   2 root  wheel   512 Jul 21 02:08 mnt
   drwxr-xr-x   2 root  wheel   512 Jul 21 02:08 net
   dr-xr-xr-x   2 root  wheel   512 Jul 21 02:08 proc
   drwxr-xr-x   2 root  wheel  2560 Jul 21 02:09 rescue
   drwxr-xr-x   2 root  wheel   512 Sep 13 02:57 root
   drwxr-xr-x   2 root  wheel  2560 Jul 21 02:10 sbin
   lrwxr-xr-x   1 root  wheel    11 Jul 21 02:11 sys -> usr/src/sys
   drwxrwxrwt   7 root  wheel   512 Sep 13 03:11 tmp
   drwxr-xr-x  17 root  wheel   512 Sep 13 02:06 usr
   drwxr-xr-x  25 root  wheel   512 Sep 13 02:40 var

First triplet is used for owner user permissions, second one is for owner group
permissions and the last one is for other users permissions.

::

   # owner can read and execute,
   # owner group can only read,
   # others can do nothing
   r-xr-----  ... file1

There is `chmod <https://linux.die.net/man/1/chmod>`_ command which is used for
permissions management.

.. code-block:: bash

   # add write permission for group:
   chmod g+w file.txt
   # add read and execute permissions for owner and group
   chmod ug+rx file.txt
   # add read permission for all
   chmod ugo+r file.txt
   # ugo can be replaced with a
   chmod a+r file.txt  # same as above

   # add write for user, read for others
   chmod u+w,o+r file.txt

Every tiplet can be represented as a bitmask:

::

   u  g  o
   rwx------ ... file.txt
   421421421

Thus in order to allow read and execute for owner and read for group we can do
the following:

.. code-block:: bash

   chmod u+rx,g+r file.txt
   chmod 540 file.txt

For directories ``x`` permission means the ability to enter the directory.

Processes
---------

**Process** is some code which is sored in the RAM and is being executed.
Most of processes are run in the background. In order to move process to
foreground there is `fg <https://linux.die.net/man/1/fg>`_ command. To move
process to background there is `bg <https://linux.die.net/man/1/bg>`_ command.
There is a possibility to start process in the background explicitly: all you
have to do is to add ampersand character at the end of command:

.. code-block:: bash

   # note the ampersand character at the end of the command
   run_my_script --arg1 --arg2=foo &

Widely used utilities to manage processes in UNIX/Linux systems are:

- `jobs <https://linux.die.net/man/1/jobs>`_ -- lists jobs running in the
  current terminal
- `nohup <https://linux.die.net/man/1/nohup>`_ -- runs the process which will
  not die after terminal is detached
- `kill <https://linux.die.net/man/1/kill>`_ -- sends signals to the processes.
  Signals which are used to stop the processes are ``SIGTERM`` and ``SIGKILL``.
  ``kill`` utility works with processes ids (PIDs)
- `killall <https://linux.die.net/man/1/killall>`_ -- similar to ``kill``, but
  works with process name.
- `top <https://linux.die.net/man/1/top>`_ -- displays Linux/UNIX processes.
- `ps <https://linux.die.net/man/1/ps>`_ -- reports a snapshot of the current
  processes. ``ps`` is usually invoked with ``aux`` keys.
- `pstree <https://linux.die.net/man/1/pstree>`_ -- displays a tree of processes
- `uptime <https://linux.die.net/man/1/uptime>`_ -- tells how long the system
  has been running.
- `free <https://linux.die.net/man/1/free>`_ -- displays amount of free and used
  memory in the system.

The Open Systems Interconnection model
======================================

:Protocol:
  is the set of rules and conventions which are used for interaction between the
  same layer of different nodes.

:Interface:
  is the set of rules which are used for interaction between adjacent layers of
  the same node

:Encapsulation:
  is the inclusion of the data from the upper layer into the special data
  structure of the lower layer. **Decapsulation** is the reverse procedure.

OSI model descibes 7 layers of network organization and the purpose of each
layer. Protocols are not described in the OSI model.

+-----+--------------+
| №   | Name         |
+=====+==============+
| 7   | Application  |
+-----+--------------+
| 6   | Presentation |
+-----+--------------+
| 5   | Session      |
+-----+--------------+
| 4   | Transport    |
+-----+--------------+
| 3   | Network      |
+-----+--------------+
| 2   | Data link    |
+-----+--------------+
| 1   | Physical     |
+-----+--------------+


OSI layers functions
--------------------

Physical layer
~~~~~~~~~~~~~~

Bit transfer via physicall channels.

- forming electric sugnals
- data encoding
- synchronization
- modulation
- physical topology
- physical characteristics of interfaces

All of these are implemented in the hardware.

Data link layer
~~~~~~~~~~~~~~~

Reliable data frame delivery between two adjacent stations in the network with
any topology or between any two stations in the network with typical topology.

- environment availability checks
- grouping data into frames
- computation and verification of the checksum
- physical addressing (MAC addresses)
- data flow management

These functions are implemented both in hardware and programmatically.

Network layer
~~~~~~~~~~~~~

Packet delivery

- between any two nodes of the network with any kind of topology
- between any two networks in the composite network
- logical addressing
- package data size coordination

:Network:
  is the set of computers which use single network technology for data
  exchange

:Route:
  is the sequence of routers which are passed by the data package in the
  composite network

Transort layer
~~~~~~~~~~~~~~

Data delivery with the determined reliability between any two processes in the
network.

- splitting message into chunks and their numeration
- buffering
- ordering of the incoming packages
- application processes addressing
- flow management
- integrity check

.. note::

   The unique identifier of process in the node in terms of TCP/IP terminology
   is called **port**

Session layer
~~~~~~~~~~~~~

.. note::

   Explicit implementation of this layer is missing in most of TCP/IP stack
   implementation. Thus only ideas of session layer are described here.

Managing application layer objects' dialog. (Synchronization between processes
on different nodes).

- Sets message exchange methods (duplex/half-duplex)
- Message exchange synchronization
- Dialog check-points

Protocol data unit of session layer is ``message``.

Presentation layer
~~~~~~~~~~~~~~~~~~

.. note::

   As well as session layer, presentation layer is not explicitly implemented in
   most TCP/IP implementations.

Coordination of data presentation for interprocess communication.

- Translates data from external format into internal format.
- Encrypts and decrypts data
- Data compression

Application layer
~~~~~~~~~~~~~~~~~

Set of all network services which can be used by the end users.

- User authentication and authorization
- File services, email, remote access, printing, etc

TCP/IP protocol stack
=====================

TCP/IP protocol stack is the implementation of the model. It includes only 4
layers:

- Application layer
- Transport layer
- Network layer
- Network interfaces layer

There are no network interfaces layer protocols in TCP/IP stack. There are only
interfaces between network and network interfaces layers.

+---------------+----------------------------------------------+
| Layer         | Protocols and standards                      |
+===============+==============================================+
| Application   | HTTP, SMTP, DNS, FTP                         |
+---------------+----------------------------------------------+
| Transport     | TCP, UDP                                     |
+---------------+----------------------------------------------+
| Network       | IP, ICMP                                     |
+---------------+----------------------------------------------+
| Network       | Ethernet, WiFi                               |
| interfaces    |                                              |
+---------------+----------------------------------------------+

IP Protocol
===========

IP (Internet Protocol) is a internetwork protocol described in `RFC 791
<https://tools.ietf.org/html/rfc791>`_.

:internet: is a joint network
:subnet: is a part of the network
:internetworking: networks union
:Internet: name of the most well-known network

Internet Protocol is the base on which Internet is built.

IP functions:

- routing
- logical addressing
- coordinating MTUs
- uniting networks
- quality of service

Header format:

.. image:: http://flylib.com/books/2/296/1/html/2/images/01fig02.jpg
   :target: http://flylib.com/books/2/296/1/html/2/images/01fig02.jpg

Control Protocols
=================

In order to debug network layer and IP (internet protocol) such protocols as
ICMP (Internet Control Message Protocol) and ARP (Address Resolution Protocol)
were introduced. Please note that ARP works between Network and Network
Interfaces layers.

There is also DHCP protocol which works on Application layer but is a auxiliary
protocol for Network Layer.

ICMP
----

Protocol specification can be found in `RFC 792
<https://tools.ietf.org/html/rfc792`_. ICMP  is mostly used as diagnostic tool
to determine whether Network layer works correctly, hovewer the original purpose
was much wider.

All information about package delivery (by IP) can be sent to the sender using
ICMP.

Earlier ICMP was used to manage network nodes (get address resolution table, set
up routing, etc), however better tools appeared later thus deprecating such
purpose of ICMP.

.. note::

   ICMP packet is icluded into the IP packet

ICMP cannot be used to debuug ICMP error messages, as the node which determines
issue with the ICMP error message must not generate ICMP message.

ICMP does not fix problems and does not retry sending messages.

Header format:

.. image:: http://processors.wiki.ti.com/images/6/61/Frame_format_icmp.png
  :target: http://processors.wiki.ti.com/images/6/61/Frame_format_icmp.png

ICMP message types:

+------+----------------------------------------------------------------------+
| Type | Description                                                          |
+======+======================================================================+
|  0   | Echo response                                                        |
+------+----------------------------------------------------------------------+
|  3   | Destination host unreachable                                         |
+------+----------------------------------------------------------------------+
|  4   | Source suppression                                                   |
+------+----------------------------------------------------------------------+
|  5   | Route redirection (Informing that better route to host exists)       |
|      | Disabled in modern systems due to security concerns                  |
+------+----------------------------------------------------------------------+
|  8   | Echo request                                                         |
+------+----------------------------------------------------------------------+
|  11  | Packet TTL expired                                                   |
+------+----------------------------------------------------------------------+
|  12  | Malformed parameters                                                 |
+------+----------------------------------------------------------------------+
|  13  | Timestamp request (Currently this is NTP functionality)              |
+------+----------------------------------------------------------------------+
|  14  | Timestamp response (Currently this is NTP functionality)             |
+------+----------------------------------------------------------------------+
|  17  | Mask request                                                         |
+------+----------------------------------------------------------------------+
|  18  | Mask response                                                        |
+------+----------------------------------------------------------------------+

ICMP Error types are different for each message type.

Most widely used tools for network diagnostics (which use ICMP) are:

- ``ping``

  This is a very simple network diagnostics tool.

  Uses ICMP message types 0 and 8. ``ping`` is used to determine concrete
  host availability in the network.

- ``traceroute``

  Shows the route to the destination host. Please note that IP protocol **does
  not** have built-in utilities for determining routes, thus tools like
  ``traceroute``  cannot be 100% precise. For example, ``traceroute`` does it by
  sequentially sending packets with increasing ttl thus generating ttl expired
  error on every host in the route.

ARP (Address Resolution Protocol)
---------------------------------

ARP is used to map IP addresses (logical addressing) to MAC addresses (physical
addressing). The protocol is described in `RFC 826
<https://tools.ietf.org/html/rfc826>`_

.. image:: http://www.erg.abdn.ac.uk/users/gorry/course/images/arp-header.gif
  :target: http://www.erg.abdn.ac.uk/users/gorry/course/images/arp-header.gif
