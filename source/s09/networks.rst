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

.. code-block::

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

.. code-block::
    u  g  o
   rwx------ ... file.txt
   421421421

Thus in order to allow read and execute for owner and read for group we can do
the following:

.. code-block:: bash

   chmod u+rx,g+r file.txt
   chmod 540 file.txt

For directories ``x`` permission means the ability to enter the directory.
