---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-03-18 20:55:26+00:00
layout: post
link: https://invisible.ch/2006/03/18/configuring-x-and-domino-server-on-debian-sarge-xen/
slug: configuring-x-and-domino-server-on-debian-sarge-xen
tags: ["blog"]
title: Configuring X and Domino Server on Debian Sarge XEN
type: post
wordpress_id: 526
---

More in my tale of the xen-server. 

My goal is to run [Lotus Domino][1] on this box, and the [last installment][2] saw the server coming up, waiting to be configured. Well, it turns out, that IBM presumes that you have X installed on your servers, because it wants to setup the server using a Java frontend. 

So, the first task is to setup X on the virtualized Host. [Giving your Xen instances a working X setup][3] takes care of that nicely. I found [Chicken of the VNC][4] to be a really nice VNC client for the Mac. Then I had some problems getting the Notes server to start, but (in turn) that's what helped me:

* chowning the /usr/local/notesdata to notes:notes
* This error thrown by the domino server

    > ""Please edit your shell's DISPLAY environment variable to 

    > reflect an unlocked terminal that you would like to launch 

    > the Domino Setup Program"" 

  was solved through [an old post on the suse mailing list][5]
* and also by doing "xhost +" as root in the virtual server [as per this post from the corner office][6]
* and a link to the [Lotus Domino 6 for Linux][7] Redbook by IBM

So this is what I get, after a lot of fiddling:

[![](https://static.flickr.com/50/114285123_8bbbb9b55c.jpg?v=0)](https://www.flickr.com/photos/jcfischer/114285123/)

Open problems:

* Can't use X11 on my Mac to connect to the X client on my Xen Server. Getting all kinds of error messages, that frankly, I don't grok (and it works with VNC, so there)
* Xen doesn't use the Swap partition I made for the Notes server. It can't find /dev/hda2...

But at least, the Domino server is up and running...

[1]: https://www-306.ibm.com/software/lotus/
[2]: /2006/03/14/installing-lotus-domino-654-in-debian-xen/
[3]: https://www.debian-administration.org/articles/322
[4]: https://sourceforge.net/projects/cotvnc/
[5]: https://lists.suse.com/archive/suse-domino/2002-Dec/0011.html
[6]: https://colinp.dominodeveloper.net/plink/040228-0138
[7]: https://publib-b.boulder.ibm.com/redbooks.nsf/RedbookAbstracts/sg246835.html?Open




Technorati Tags: [debian](https://www.technorati.com/tag/debian), [domino](https://www.technorati.com/tag/domino), [lotus notes](https://www.technorati.com/tag/lotus notes), [xen](https://www.technorati.com/tag/xen)
