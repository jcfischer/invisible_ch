---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-09-28 00:33:34+00:00
layout: post
link: https://invisible.ch/2003/09/28/saving-a-dell/
slug: saving-a-dell
tags: ["blog"]
title: Saving a Dell
type: post
wordpress_id: 187
---

The display on my Inspiron 8200 has gone from slightly flaky to totally unusable in a matter of only two days. It started with odd colors during boot - it looked like the red has gone. Then some syncing errors cropped up. After a couple of seconds it would be ok... Now the display has gone compeletely nuts and the beautyfull 1600x1200 pixel display just displays white, out-of-sync lines.

Couple that with an increasing number of Windows XP blue screens - and it means you are looking at a lot of trouble. XP blue screens right after booting - and I can't read what went wrong. The secure startup mode still works, but network, USB and FireWire don't work.

And of course there are gigabytes of data that aren't saved completely (because the external 200GB FireWire drive I bought for exactly the purpose of backing up this laptop seems to have a problem on XP. "I'll get to that later", I said to a colleague this last thursday...

Well - time has come to move faster. This laptop needs to see the interior of a Dell workshop as fast as possible and I need my data off of it before that.

Knoppix to the rescue! (Avid readers know that I have Debian installed on this machine, but I never managed to build a kernel that recognizes my external FW disk, so even that option was out...)

I brought out my [Knoppix](https://www.knoppix.org) CD and booted from it. Of course it wouldn't recognize the FireWire HDD either (and no - it didn't recognize it as a USB disk too). Some reading on the Knoppix forums led me to the secret sauce:

Drop to a Root console

    
    # modprobe ieee1394
    # modprobe ohci1394


Plug in the FireWire disk and see that something happens on the console. Do 

    
    # fdisk -l


and notice the /dev/sda1 device that has materialized.

    
    # mkdir /mnt/sda1
    # mount -t vfat /dev/sda1 /mnt/sda1


My NTFS and FAT partitions were already mounted, so I looked up the [TAR parameters](/archives/000098.html) and started to back up my stuff:

    
    # hdparm -d1 /dev/hda
    # cd /mnt/sda1
    # tar -cvzf directory-stuff.gz /mnt/hda5/directory/stuff
    # tar -cvzf directory.gz /mnt/hda5/directory/ --exclude stuff/*
    # ...


Lessons learnt:

  * TAR has a upper filesize limit of 2GB - even compressing 20GB of c:\ doesn't fit into 2 gigs
  * Groove takes a loooot of storage space
  * It pays to enable DMA mode on your drives before you start reading large amounts of data from it
  * Backups should be done when you have machinery that is in good working conditions

It looks like I'm going to be OK - and only losing a lot of time and my laptop for a couple of days... Wheeew
