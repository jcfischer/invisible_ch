---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-06-13 10:03:59+00:00
layout: post
link: http://blog.invisible.ch/2013/06/13/rescueing-a-non-booting-vm-under-openstack/
slug: rescueing-a-non-booting-vm-under-openstack
tags: ["blog"]
title: Rescueing a non booting VM under Openstack
type: post
wordpress_id: 12903
---

So we are running an OpenStack installation based on Folsom, but with Ceph as our underlying storage engine for volumes. This is a bit cutting edge. To make matters more bleeding, we run the Ceph OSDs on BTRFS - definitively bleeding edge, as we had various of our servers die with BTRFS related kernel panics. The advice usually given is to upgrade the BTRFS code - so we have started to migrate our Quantal (12.10) servers to Raring (13.04)

One of the reasons, our systems fall over (we assume) is that we run quite disk heavy things on our VMs. After the update of one of the physical hosts to Raring, the "most important" virtual machine decided it wouldn't boot anymore:

[![Dead virtual machine](http://blog.invisible.ch/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-08.45.02-300x180.png)](http://blog.invisible.ch/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-08.45.02.png)It could be, that this due to a different kernel on the physical machine, than on the host - although that seems highly unlikely. Anyway - what now? The usual forum links point to a situation, where you can either boot the system, or access the disk by booting into a rescue system - neither option works in a virtualized environment.

But, there is hope: You can mount the image and try to perform operations on it. The [OpenStack Operations Manual](http://www.valleytalk.org/wp-content/uploads/2013/03/OpenStackOperationsGuide.pdf) (p 106ff) has informations on how to mount a disk and read from it, if you want to write, you will have to do a bit more:\

    
    kvm-nbd --connect=/dev/nbd0 /var/lib/nova/instances/instance-000000af/disk
    mount -rw /dev/nbd0p1 /mnt
    
    mount --bind /dev/ /mnt/dev
    chroot /mnt/ /bin/bash        # from now on, you are inside the mounted disk
    mount -t proc none /proc
    mount -t sysfs none /sys
    # do your stuff
    exit                          # and back on the physical host
    umount /mmt/dev /mnt/proc /mnt/sys
    kvm-nbd -d /dev/nbd0


**NOTE**: Don't edit stuff on the mounted filesystem if you haven't done the chroot command. You will mess up the files (and the owner information) and will leave files that cannot be edited or removed...

For all the editing we did, we never managed to get the VM into a state where it worked again. The snapshot done yesterday had the same failing behaviour. We will therefore rebuild the VM.

Oh well, sometimes you win, sometimes you loose. (We didn't loose any data though - that is stored on a volume outside of the VM)
