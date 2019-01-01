---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-11-24 08:43:41+00:00
layout: post
link: https://invisible.ch/2006/11/24/rails-on-synology-cubestation-cs-406/
slug: rails-on-synology-cubestation-cs-406
tags: ["blog"]
title: Rails on Synology CubeStation CS-406
type: post
wordpress_id: 570
---

Preparing for my [workshop][1]

## Enable Telnet Access

see [Oinkzwurgels page][2], download 'syno-telnet-r3.zip' and install it in the Synology Web Admin panel. The installation will stop at 99% - that's fine

Now you can telnet to the CubeStation:

    $ telnet 192.168.x.y
    CubeStation login: admin
    Password: 

    BusyBox v1.1.0 (2006.08.06-13:52+0000) Built-in shell (ash)
    Enter 'help' for a list of built-in commands.

    CubeStation> ls

You can login as any user you created. For the following steps, login as root (same password as your admin account)

Bingo!

## install the ipgk stuff

Again - from Oinkzwrurgels document:

    CubeStation> cd /tmp
    CubeStation> wget https://oinkzwurgl.org/dl.php?file=bootstrap-ppc.tar.gz
    ...
    CubeStation> cd /
    CubeStation> tar -xzvf /tmp/bootstrap-ppc.tar.gz 
    ...
    CubeStation> ln -s /volume1/opt /opt
    CubeStation> export PATH=/opt/bin:/opt/sbin:$PATH
    CubeStation> /opt/bin/ipkg update
    CubeStation> /opt/bin/ipkg upgrade

## More software

    CubeStation> /opt/bin/ipkg list | grep ruby                                                                                                                         
    ruby - 1.8.5-1 - An interpreted scripting language for quick and easy object-oriented programming.
    rubygems - 0.9.0-1 - Ruby packaging and installation framework.

    CubeStation> ipkg install zlib
    CubeStation> ipkg install ruby
    CubeStation> ipkg install rubygems

I then installed the native toolchain as described on Oinkzwurgels pages

    CubeStation> ipkg install make


## Rails?

    CubeStation> gem install rails --include-dependencies

Prepare a cup of coffee and wait. Get some more coffee. Do some chores. Go to sleep.

Update /root/.profile so that the PATH is set to include /opt/local/bin

Here's my current:

    #/etc/profile: system-wide .profile file for ash.
    PATH="$PATH:/bin:/sbin:/usr/bin:/usr/sbin:/usr/syno/bin:/usr/syno/sbin:/usr/local/bin:/usr/local/sbin:/opt/bin:/opt/sbin"
    umask 022
    #This fixes the backspace when telnetting in.
    #if [ "$TERM" != "linux" ]; then
    #        stty erase
    #fi
    export PATH
    HOME=/root
    export HOME
    TERM=${TERM:-cons25}
    export TERM
    PAGER=more
    export PAGER
    PS1="`hostname`> "
    alias dir="ls -al"
    export CFLAGS="/opt/include:/opt/crosstool/gcc-3.4.5-glibc-2.3.3/powerpc-603-linux-gnu/powerpc-603-linux-gnu/include"
    export CXXFLAGS="$CFLAGS"
    export LDFLAGS="-L/opt/lib"
    export PATH="$PATH:/opt/crosstool/gcc-3.4.5-glibc-2.3.3/powerpc-603-linux-gnu/bin/"
    export PATH="$PATH:/opt/local/bin"
   
Let's try it:

    CubeStation> mkdir -p /volume1/test
    CubeStation> cd /volume1/test
    CubeStation> rails cube
    ...
   
If all goes well, the rails command should create the directory structure for a project.

    CubeStation> cd cube
    CubeStation> ruby script/server

starts Webrick and you can access your page through the webbrowser at https://192.168.x.y:3000

Tata.

## Mongrel

So far I haven't been able to install mongrel. The compilation fails because of

* wrong paths in makefile (fixable)
* missing syslimits.h header file (haven't been able to track that down yet)

## Next steps

Getting a real application with database access up and running

## More software?

Oh yes - the [NLSU2][3] page has more [packages][4]. So far I have installed:

* mt-daap - the iTunes server
* openSSH - no telnet for me, thanks


 

[1]: /2006/11/20/speaking/
[2]: https://oinkzwurgl.org/diskstation
[3]: https://www.nslu2-linux.org/wiki/DS101/HomePage
[4]: https://www.nslu2-linux.org/wiki/Optware/Packages 
