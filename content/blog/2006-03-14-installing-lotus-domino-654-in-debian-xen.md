---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-03-14 22:27:37+00:00
layout: post
link: http://invisible.ch/2006/03/14/installing-lotus-domino-654-in-debian-xen/
slug: installing-lotus-domino-654-in-debian-xen
tags: ["blog"]
title: Installing Lotus Domino 6.5.4 in Debian XEN
type: post
wordpress_id: 525
---

Get the 6.5.4 TAR file from [notes.net][1] and copy it to your Debian server.

Here's my /etc/xen/notes.cfg:

    kernel = "/boot/vmlinuz-2.6.12-xenU"
    memory = 384 
    name   = "notes"
    root   = "/dev/sda1 ro"
    vif    = ['mac=00:00:00:00:00:01, bridge=xenbr0' ]
    disk   = [ 'file:/home/xen/domains/notes/data.img,sda1,w',  'file:/home/xen/domains/notes/swap.img,sda2,w' ]

To distinguish in which environment to type the following commands: host # means the "physical" host machine while notes # means that you are in a shell in the virtual domain.

I have a disk image for my Xen Notes Server, so I did:

    host# mount -t ext3 -o loop /home/xen/domains/notes/disk.img /mnt/disk
    host# cd /mnt/disk/usr
    host# tar xfv /path/to/download/notes-server.tar
    host# umount /mnt/disk
    host# xm create -c notes.cfg

Then do the Debian Base Configuration in your virtual machine

    notes# base-config
    notes# adduser notes
    notes# apt-get install ssh
    notes# shutdown -h now

Back in the hosts machine:

    host# mount -t ext3 -o loop /home/xen/domains/notes/disk.img /mnt/disk
    host# chroot /mnt/disk /bin/bash
    host# mv /lib/tls /lib/tls.disabled
    host# cd /usr/local/linux
    host# ./install

This will start the Notes Server installation. For some strange reason, the install fails inside the virtual machine. It complains about the terminal size not being set correctly...
I installed the server to */opt/lotus* and the data to */usr/local/notesdata*. After the installation has completed

    host# exit

to get back to the real host and unmount the disk-image
    
    host# umount /mnt/disk

Time to start the virtual machine with the installed Domino server...

    host# xm create -c notes.cfg

login as notes and try to start the server

    notes$ cd /usr/local/notesdata
    notes$ /opt/lotus/bin/server -listen

which will result in an error message 

    /opt/lotus/notes/latest/linux/server: error while loading shared libraries: libstdc++-libc6.1-1.so.2: cannot open shared object file: No such file or directory

The library needed is old, and not included in the current debian release. Unfortunately the [excellent notes by Ian Cherril][2] only cover an automated installation with apt-get which will no longer work. Therefore we need to hunt down the paket somewhere on the internet:

    notes$ su -
    notes# wget http://ftp.debian.org/pool/main/e/egcs1.1/libstdc++2.9-glibc2.1_2.91.66-4_i386.deb
    notes# dpkg -i libstdc++2.9-glibc2.1_2.91.66-4_i386.deb
    notes# exit
    notes$ /opt/lotus/bin/server -listen

and: Bingo, it starts!

Coming up - configuring the server

   

[1]: http://www.notes.net
[2]: http://www-10.lotus.com/ldd/nd6forum.nsf/55c38d716d632d9b8525689b005ba1c0/20fda6ee3399510085256df7003d5005?OpenDocument

