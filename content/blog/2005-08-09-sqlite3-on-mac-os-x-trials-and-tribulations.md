---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-08-09 13:10:59+00:00
layout: post
link: http://blog.invisible.ch/2005/08/09/sqlite3-on-mac-os-x-trials-and-tribulations/
slug: sqlite3-on-mac-os-x-trials-and-tribulations
tags: ["blog"]
title: sqlite3 on Mac OS X -- trials and tribulations
type: post
wordpress_id: 445
---


For an upcoming Rails project, the plan is to [use ](http://wiki.rubyonrails.com/rails/show/HowtoUseSQLite)the [sqlite](http://sqlite.org/) database. On  Windows, the whole process of getting this installed was easy. Download the DLL, do a gem install sqlite3& and be done.



Not so on OS X, where I plan to develop.



sqlite3 is installed by default, but trying to install the gem, I get a complaint about a missing sqlite.h file. Fair enough, it's probably not there. So I download the tarball and do the "./configure && make && make install" dance.



I end up with this error message:



/usr/bin/libtool: for architecture: cputype (16777234) cpusubtype (0) file: -lSystem is not an object file (not allowed in a library)



some [googling later](http://www.google.com/search?hl=de&client=safari&rls=de-de&q=mac+file%3A+-lSystem+is+not+an+object+file+%28not+allowed+in+a+library%29&btnG=Suche&lr=), it [seems to be related](http://gentoo-wiki.com/Gentoo_MacOS) to wrong file permissions, so I repair the volumes file permissions (using the Mac Disc Utility). Re-running "make" yields the same error message.



Incidentally, this is the same error message I got, when I tried to use the Darwin Ports to install sqlite. So I guess, something in my system is hosed.



**Update 1: **The fix for compiling & linking was as easy as installing the Tiger version of the XCode Tools from the Tiger CD. Back when I upgraded to Tiger, I didn't install them. 



**Update 2: **When installing sqlite3, also install the sqlite3 gem: sudo gem install sqlite3-ruby



To be continued





Technorati Tags: [mac](http://technorati.com/tag/mac), [rails](http://technorati.com/tag/rails), [sqlite](http://technorati.com/tag/sqlite)
