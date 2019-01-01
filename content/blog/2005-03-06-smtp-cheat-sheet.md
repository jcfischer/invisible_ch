---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-03-06 20:54:38+00:00
layout: post
link: http://invisible.ch/2005/03/06/smtp-cheat-sheet/
slug: smtp-cheat-sheet
tags: ["blog"]
title: SMTP Cheat Sheet
type: post
wordpress_id: 383
---

From the "my external memory dept":

One of the simplest way to debug SMTP problems is to talk directly to the SMTP server using a shell (Telnet):

    
    Frodo:~ jcf$ telnet smtp.domain.ch 25
    Trying xxx.xxx.xxx.xxx...
    Connected to smtp.domain.ch.
    Escape character is '^]'.
    220 smtp.domain.ch ESMTP ready.
    MAIL FROM:name@domain.ch 
    250 OK
    RCPT TO:joe@doe.com
    250 Accepted 
    DATA
    354 Enter message, ending with "." on a line by itself

and then the message you want to send (including the headers)
