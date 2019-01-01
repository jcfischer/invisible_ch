---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-03-31 21:15:42+00:00
layout: post
link: https://invisible.ch/2005/03/31/notes-domino-server-crashes-and-fixup-woes/
slug: notes-domino-server-crashes-and-fixup-woes
tags: ["blog"]
title: Notes / Domino Server crashes and fixup woes
type: post
wordpress_id: 398
---

I'm sitting in front of two clustered Notes servers that have died on me when I tried to diagnose a problem using the [OpenLog][1] log database. I added some unsupcious looking code to circumvent a problem that of course failed. In order to get more informtation on what failed, I decided to use OpenLog to pinpoint the error. 

The moment, the agent ran with OpenLog enabled the Domino 6.0.4 server died. The following restart had it hanging on a consistency check. Killing the server with `nsd -kill`and a subsequent `nfixup -j -S c:\domdata` brought up a lot of "interesting" error messages:

    Hardware/OS error () writing to database (c:\Domdata\xx\xxxx.NSF), 
    Length=5B8 (PID=2D8/TID=2)

This is on a Windows 2003 Server.

Has anyone got any clue of what is going on?

(In the meantime I have managed to kill the clustered backup server in the same manner and I'm looking at it fixuping it's databases before I can restart it)

It's going to be a long night....

[1]: /archives/000384.html
