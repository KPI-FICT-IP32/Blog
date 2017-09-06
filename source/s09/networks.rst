====================
Network technologies
====================

:Lecturer: `Rokovyi Oleksandr Petrovych <http://comsys.kpi.ua/ukrainian/teachers/57/>`_

.. contents::
   :depth: 3

--------------

Lecture #1. Linux and UNIX systems
==================================

.. note::
    further UNIX/Linux denotes all Linux, UNIX, Linux-like and UNIX-like systems

UNIX ideology
-------------

- There are two types of resources: files and processes. However file entity is 
  much wider than one in Windows systems. Hardware devices, IPC mechanisms, etc
  are represented as files. There are 6 types of files:

  - Regular file
  - Directory
  - Device

    - Block device
    - Char device
  - Socket
  - Pipe (IPC mechanism)
  - Link

    - Hardlink
    - Symlink

  This allows to manage everything in one way: by changing permissions on the
  filesystem level.

- Filesystem hierarcy is important. It is represented as a tree, which starts
  from root (``/``). The mechanism behind the hierarcy is simple directories.

  There is a filesystem struture standard which defines where the parts of
  operating system are located, where which kinds of files are located, etc.
