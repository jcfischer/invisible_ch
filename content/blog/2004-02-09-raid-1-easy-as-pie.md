---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-02-09 18:46:13+00:00
layout: post
link: http://invisible.ch/2004/02/09/raid-1-easy-as-pie/
slug: raid-1-easy-as-pie
tags: ["blog"]
title: RAID 1 - easy as pie
type: post
wordpress_id: 246
---

This server was down a bit during the day when I installed the new 3Ware RAID IDE Controller and moved a couple of directories to a mirrored disk. The process was more or less painless but I learnt a couple of interesting tid-bits.

**Computers don't turn themselves on, when they don't have power.** That means - if nothing happens on pressing the BRS, check that the connector from the power supply is firmly seated in the motherboard. (Turns out that I partially unplugged mine when fumbling with additional IDE cables.

**A midi tower is not enough for a server** Nobody thought that a midi sized PC would have more than 2 IDE 3.5" drives, so no provisions are made to add more. With some creative use of existing space, a folded piece of paper as electrical insulation and hope that nobody will rattle the box too much, the second mirrored drive lies in a 3.5" floppy bay (of which there are two for some reason, but no provions for holding a harddisk. Go figure.

**RAID is simpler than it seems** Power up the computer, go to the RAIDs card BIOS, select the two drives, select create RAID1, select Done. The Linunx installation recognizes a 3Ware driver. At a root prompt "/dev/sda" which automagically loads the SCSI drivers (this RAID looks like a SCSI disk to the OS), fdisk to create partitions, mount it, mkreiserfs,  copy the data over, enter the new paths in /etc/fstab instead of the old ones, reboot - done.

**You should update your blog** I know how to solve the [slowness of this server](/archives/000061.html) I blogged about it - but I didn't enter all necessary information. Bad. The blog is my external memory, so I'd better keep it up to date.... (which I have done now)
