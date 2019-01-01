---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-10-28 20:29:52+00:00
layout: post
link: http://blog.invisible.ch/2007/10/28/rails-stack-on-leopard/
slug: rails-stack-on-leopard
tags: ["blog"]
title: Rails Stack on Leopard
type: post
wordpress_id: 634
---

Yes, Leopard is that great, but getting a full Rails Stack working again is a lot of work....

(work in progress)

### Ruby / Rails


* Ruby and Rails are bundled with Leopard. Be sure to read about the Apple modifications [What's new in Leopard][6]
* The rails command defaults to sqlite as it's database. Use:


    $ rails -d mysql project_name


### MySQL

* Download 10.4 package from [MySQL][2] and install both the mysql and the startupitem.
* Start/Stop doesn't work, use [these instructions][4]
* apply the fixes from [AngryFly][5]

### MacPorts

* Download and install [MacPorts 1.5.0-10.5.dmg][3]

### Git

    $ sudo port install git-core

### SSH

I have strange errors when the MacPorts version of SSH was being used (no connections, git didn't pull from remote servers). I "solved" it by renaming it:

    $ sudo mv /opt/local/bin/ssh /opt/local/bin/ssh_old

### Subversion

* SVN is bundled in Leopard

### ImageMagic

* following the instructions at [NullStyle][1]

### Postgres

Here's the [secret sauce to not only make Postgres compile, but also include DTrace support][7] - alas it still doesn't work for me...

Here's the munged ./configure line, in case you want to try it: 

    $ sudo ./configure --sysconfdir=/opt/local/etc/postgresql82 --bindir=/opt/local/lib/postgresql82/bin --libdir=/opt/local/lib/postgresql82 --includedir=/opt/local/include/postgresql82 --datadir=/opt/local/share/postgresql82 --mandir=/opt/local/share/man --without-docdir --with-includes=/opt/local/include --with-libraries=/opt/local/lib --with-openssl --with-bonjour --with-readline --with-zlib --enable-thread-safety --enable-integer-datetimes --enable-dtrace

I have exactly the same error as [here][8]. Hmm, download the Postgres sources? 

Finally: A [combination][7] of [instructions][9] got me up and running: (get the DTrace patches and the Postgres Source. Unpack the DTrace patch)

    $  sudo port install postgresql82 postgresql82-server

fails as expected

    $ cd  /opt/local/var/macports/build/_opt_local_var_macports_sources_rsync.macports.org_release_ports_databases_postgresql82/work/postgresql-8.2.5
    $ cat ~/Desktop/Inbox/postgresql-825-fixosxdtracediff | patch -p1  
    $ tar xvjf ~/Desktop/Inbox/postgresql-8.2.5.tar.bz2 
    $ sudo cp -r postgresql-8.2.5/src/ src/
    $ sudo ./configure --sysconfdir=/opt/local/etc/postgresql82 --bindir=/opt/local/lib/postgresql82/bin --libdir=/opt/local/lib/postgresql82 --includedir=/opt/local/include/postgresql82 --datadir=/opt/local/share/postgresql82 --mandir=/opt/local/share/man --without-docdir --with-includes=/opt/local/include --with-libraries=/opt/local/lib --with-openssl --without-bonjour --with-readline --with-zlib --enable-thread-safety --enable-integer-datetimes 
    $ sudo make
    $ cd ~
    $ sudo port install postgresql82
    $ sudo port install postgresql82-server

notice that even though I apply the DTrace patch, I overwrite it in the next line. The ./configure does not enable DTrace. Maybe that part wouldn't be necessary? Dunno - that was the sequence that compiled and installed for me.

Configure the server:

    $ sudo mkdir -p /opt/local/var/db/postgresql82/defaultdb
    $ sudo chown postgres:postgres /opt/local/var/db/postgresql82/defaultdb
    $ sudo su postgres -c '/opt/local/lib/postgresql82/bin/initdb -D /opt/local/var/db/postgresql82/defaultdb'
    $ sudo launchctl load -w /Library/LaunchDaemons/org.macports.postgresql82-server.plist


### Ruby Postgres Gem

Home stretch... Based on [Carl Gaywoods instructions][10], here are the commands to install the Postgres Gem with Apples Ruby and the MacPorts Postgres:

    $ sudo gem install postgres
    $ cd /Library/Ruby/Gems/1.8/gems/postgres-0.7.1/
    $ sudo ruby extconf.rb --with-pgsql-include=/opt/local/include/postgresql82 --with-pgsql-lib=/opt/local/lib/postgresql82
    $ sudo make
    $ sudo make install
    $ sudo gem install postgres





[1]: http://nullstyle.com/2007/10/27/how-to-build-imagemagick-and-install-rmagick-with-macports-on-mac-os-x-leopard/
[2]: http://dev.mysql.com/downloads/mysql/5.0.html
[3]: http://svn.macosforge.org/repository/macports/downloads/MacPorts-1.5.0/
[4]: http://www.simplisticcomplexity.com/2007/10/27/start-and-stop-mysql-in-mac-os-x-10-5-leopard#comments
[5]: http://angry-fly.com/index.cfm/2007/10/26/Fix-for-MySQL-on-Leopard
[6]: http://trac.macosforge.org/projects/ruby/wiki/WhatsNewInLeopard
[7]: http://leenux.org.uk/dtrace-patches/dtrace-with-postgres-on-osx/
[8]: http://www.nabble.com/Compiling-postgresql82-on-Leopard-t4697604.html
[9]: http://www.gelens.org/2007/10/29/postgresql_in_leopard_using_ma
[10]: http://www.carlgaywood.co.uk/blog/installing-ruby-on-rails-with-postgresql
