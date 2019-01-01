---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-03-09 20:50:41+00:00
layout: post
link: https://invisible.ch/2006/03/09/installing-xen-30-on-debian-sarge/
slug: installing-xen-30-on-debian-sarge
tags: ["blog"]
title: Installing XEN 3.0 on Debian Sarge
type: post
wordpress_id: 523
---

[Sauron][1], my faithful basement server got another 512MB of RAM, and I plan to virtualize it to run multiple servers on it (most notably a Lotus Domino Server).

This is the "step by step" account of how to install [XEN 3.0][2] on it

1. Fixing the size of the root partition
   My root partition was just a tad too small, so I was stuck with the installation. The solution is rather simple:
   * Boot a Linux Live CD (I used ubuntu)
   * use parted to resize the partitions. (The [parted user guide][5] is really helpful)

2. [Installing Xen 3.0 upon Debian Sarge][3]
   Replace the 3.0.0 reference with 3.0.1 to get the current version.
   This just works (if your root partition is large enough)
3. Installing a virtual xen domain
   I used the [xen-tools][6] to create an image. While booting this image, everything seemed to go smooth until the prompt was supposed to appear. Then the virtual domain just froze. Right now, I'm trying to recreate an image without any help, to see if that will help. The [linuxwiki.de/Xen][4] entry has a step by step instruction how to create the necessary disk images. 
   Still no joy, my virtual machine boots and then hangs.

4. Suse image works
   The image found on the [suse images page][7] worked, so I know, that everything is working.

5. *Waiting*
   When I leave my virtual Debian machine starting and wait for some time, I get some new error messages:
   
    
    <code>
           INIT: Id "1" respawning too fast: disabled for 5 minutes
    
           ...
    
           INIT: Id "6" respawning too fast: disabled for 5 minutes
    
           INIT: no more processes left in this runlevel
       </code>


   Googling for this error, brings me to this [Xen Installation][8] page, where the final hint is:

   Changing the getty line in /etc/inittab to


       1:2345:respawn:/sbin/getty 38400 console    
   
   where it says "console" instead of "tty" makes my virtual domain boot.



Random Xen Documentation:

* [https://linuxwiki.de/Xen][4]

[1]: /2004/08/30/welcome-to/
[2]: https://www.xensource.com
[3]: https://www.debian-administration.org/articles/304
[4]: https://linuxwiki.de/Xen
[5]: https://www.gnu.org/software/parted/manual/html_chapter/parted_2.html
[6]: https://www.steve.org.uk/Software/xen-tools/
[7]: https://www.suse.de/~garloff/linux/xen/images/
[8]: https://www.pug.org/index.php/Xen-Installation







Technorati Tags: [debian](https://www.technorati.com/tag/debian), [sauron](https://www.technorati.com/tag/sauron), [xen](https://www.technorati.com/tag/xen)
