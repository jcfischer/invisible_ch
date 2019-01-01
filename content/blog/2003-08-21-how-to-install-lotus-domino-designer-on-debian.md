---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-08-21 16:08:03+00:00
layout: post
link: https://invisible.ch/2003/08/21/how-to-install-lotus-domino-designer-on-debian/
slug: how-to-install-lotus-domino-designer-on-debian
tags: ["blog"]
title: 'How-To: Install Lotus Domino Designer on Debian'
type: post
wordpress_id: 167
---

I have bought and installed [Crossover Office](https://https://www.codeweavers.com/products/office/) to run IE 6 and Lotus Notes on Linux. There is an installation option for Lotus Notes by default, but it failed me when I tried to install the Domino Designer and Adminstration clients.
This is what I did to get it to work and to have a shared Windows / Linux Installation of Notes:
I assume that you have a working Notes installation under Windows. Also you must be able to mount the filesystem that this installaiton resides on
Install the Lotus Notes client only in CrossOver Office. Run it, and be sure that it comes up. You can try to configure the client but we will kill that installation in a minute.
Exit Lotus Notes
Drop to a shell and go to
    
    cd ~/.cxoffice/dotwine/fake_windows/Lotus
    mv Notes Notes.back
    cp -r /mnt/windows/Lotus/Notes/*  .


If your data directory is beneath Lotus/Notes then it will be copied also (which is not what we want ultimately)
Check the ownership of all the files. Chown, chgrp and chmod until a normal user has rw access on the normal files and execute access on the *.exe files
check to see that the .NSF files are read/wreitable as well
Start Windows Application / Lotus Application / Lotus Notes in X
Notes should come up with all the clients you had under windows
Open a few databases to make sure that everything runs.
Exit Notes
This set up has the drawback, that your data directories are going to go out of sync when you work in both Windows and Linux environments.
Here's what I did: I moved my data directory to a FAT partiion that can be accessed from both operating systems. In Windows, I moved the Notes Data path (in Notes.ini) to i:\lotus\notes\data.
In Linux, the drive is mounted on /mnt/shared so the path to the directory is /mnt/shared/lotus/notes/data
In a shell do the following in your linux Notes directory

    
    mv Data Data.back
    ln -s /mnt/shared/lotus/notes/data


Start Notes again - now you should have access to the Notes data directory on your shared partition.
I had problems at first, because the ownership of the data directory was all wrong. Also the /mnt/shared mount-point was set to only allow root to access the drive - which is not really what you want.
But now I have the Notes Designer running happily under Linux
