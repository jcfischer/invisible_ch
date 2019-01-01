---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2003-09-03 12:24:48+00:00
layout: post
link: http://invisible.ch/2003/09/03/email-heaven/
slug: email-heaven
tags: ["blog"]
title: EMail heaven
type: post
wordpress_id: 173
---

I have dabbled for a long time to set up my perfect email environment. Now it slowly comes together... 
Here are the advantages of my setup:

  * access to my complete email from everywhere where I have internet access
  * Fulltext search and auto classifiying
  * Almost spam free
  * virus free
  * Managment free


Interested? Here's what you need:
  * A Linux server under your control (mine is a redhat box)
  * [Zoe](http://guests.itvectors.it/zoe/)
  * [Popfile](http://popfile.sourceforge.net/)
  * [Opera 7.x](http://www.opera.com/)

Read on for the setup
<!-- more -->
  


### Server Installation


Install PopFile and Zoe on your linux box. (I will leave that as an excercise to the reader).
I made start/stop script for both and now, both PopFile and Zoe start automatically when my Linux box restarts. You can dowload them here:[popfile](/files/popfile.txt) and [zoe](/files/zoe.txt). Copy them to your /etc/init.d directory and adapt the paths to match your systems. Then use your distributions mean of activating them in the rc. scripts.
Now you can start and stop popfile and zoe by f.e. issuing /sbin/service zoe start or /sbin/service popfile stop.
  


### Firewall Installation


Punch a hole in your firewall for the following ports:

  * 8080: the PopFile Userinterface
  * 10025: the ZOE SMTP Server
  * 10110: the ZOE POP Server (if desired - I don't have that)
  * 10080: the ZOE HTTP Server used for the interface
  * 10123: the ZOE RPC Server (if desired)

Start both Popfile and Zoe and start your webbrowser to configure the two applications.
  


### Configuration


Configure Popfile to _Accept POP3 connections from remote machines_ and _Accept HTTP (User Interface) connections from remote machines_. Both can be found on Popfiles "Security" tab.
Be sure to set a _User Interface Password_.
Configure a Zoe account and let it retrieve mail from popfile, by setting it to use localhost and the "pop.isp.com:user@name" for the login name to the ISP's Popserver. See [Here is an example](http://www.invisible.ch/images/zoe-config.html) of my setup.
Now Zoe pulls mails from PopFile which does all the Spam filtering. Zoe is the archive, and if I'm on the road, I can use the new "limited composer" to reply to or create new emails.
  


### Opera Configuration


M2 is Opera's excellent email client. Actually it has a lot of common with Zoe in that it auto-categorizes my email based on my active contacts, threads, labels, attachments, mailing lists and so on.
I use it as the full featured mail client for my regular email duties. As soon as I have processed an email, I delete it, knowing that Zoe is there to serve as my repository. Opera is also configured to pull mail from PopFile. I could use the POP server built into Zoe instead, but I don't want to re-load all 11'000 mails that Zoe holds for me at the moment. 
Because both Zoe and Opera leave the mail on the POPserver I have to clean that out from time to time - a task which could be automated some day.
