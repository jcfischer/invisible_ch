---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-03-21 21:44:48+00:00
layout: post
link: http://blog.invisible.ch/2013/03/21/48-tiny-tiny-rss-on-synology/
slug: 48-tiny-tiny-rss-on-synology
tags: ["blog"]
title: 48 - Tiny Tiny RSS on Synology
type: post
wordpress_id: 12705
---

In my quest to "[own my own data](http://blog.invisible.ch/2013/03/18/51-own-your-data/)" I spent the last few days to get an alternative to Google Reader going. I decided on trying [Tiny Tiny RSS](http://tt-rss.org/) instead of [Fever](http://feedafever.com/) mainly because TT-RSS is supported and in active development, while Fever (while looking more interesting) has been on hold for a few years and Shaun Inman basically hinted that he will not update or support it in the near future at least. Also, [Ràmon](http://blog.psy-q.ch/) has endorsed it...

Here's a walk through of getting TT-RSS  running on my Synology NAS with Postgres as the database.

[**Update**: 30.3.2013: updated to 1.7.5 and added a missing psql statement to create a user as well as new --feeds syntax for update job]

Open a shell on the Synology and download the tar

    
    wget --no-check-certificate https://github.com/gothfox/Tiny-Tiny-RSS/archive/1.7.5.tar.gz
    tar xvf Tiny-Tiny-RSS-1.7.5.tar.gz


Postgres on the Synology is not the database for users (that would be MySQL), so we need to jump through a few hoops to give a web application access to Postgres. Namely the code needs to be in /usr/syno/synoman/phpsrc

    
    mv Tiny-Tiny-RSS-1.7.5 /usr/syno/synoman/phpsrc/tt-rss
    chmod 755 -R /usr/syno/synoman/phpsrc/tt-rss


Now we need to tell Apache about that directory:

    
    vi /usr/syno/apache/conf/extra/httpd-autoindex.conf-user


Add the following line

    
    Alias /tt-rss "/usr/syno/synoman/phpsrc/tt-rss"


and restart Apache

    
    /usr/syno/etc/rc.d/S97apache-user.sh restart


Now let's create the database user and the database

    
    /usr/syno/pgsql/bin/psql -U admin postgres



    
    > CREATE USER ttrss WITH PASSWORD 'secret_password';
    > \q



    
    /usr/syno/pgsql/bin/psql 
    /usr/syno/pgsql/bin/createdb -O ttrss -E UTF8 -U admin ttrssdb 
    /usr/syno/pgsql/bin/psql -U ttrss -d ttrssdb -f /usr/syno/synoman/phpsrc/tt-rss/schema/ttrss_schema_pgsql.sql


(Optionally restart Postgres:

    
    /usr/syno/etc/rc.d/S20pgsql.sh restart


)

Now configure databas ename and user:

    
    mv /usr/syno/synoman/phpsrc/tt-rss/config.php-dist /usr/syno/synoman/phpsrc/tt-rss/config.php
    vi /usr/syno/synoman/phpsrc/tt-rss/config.php


and edit the following entries

    
    define('DB_TYPE', "pgsql"); // or mysql
    define('DB_HOST', "localhost");
    define('DB_USER', "ttrss");
    define('DB_NAME', "ttrssdb");
    define('DB_PASS', "secret_password");
    // define('DB_PORT', '5432'); // when neeeded, PG-only


We are almost there....

    
    chown -R nobody:nobody /usr/syno/synoman/phpsrc/tt-rss/cache
    chown -R nobody:nobody /usr/syno/synoman/phpsrc/tt-rss/lock
    chown -R nobody:nobody /usr/syno/synoman/phpsrc/tt-rss/feed-icons


There are two incompatibilities with the Synology PHP installation... open_basedir should be disabled (but I don't know what would break if I'd disable it). So I have just switched off the sanity check of tt-rss (nobody could say what problems tt-rss has with that...)

open_basedir:

    
    vi /usr/syno/synoman/phpsrc/tt-rss/include/sanity_check.php



    
    // if (ini_get("open_basedir")) {
    // array_push($errors, "PHP configuration option open_basedir is not supported. Please disa
    // }


Finally, the background tasks for updating the feeds need to have the mb_internal_encoding() function which is only available to root in Synology. That is easy to fix:

    
    chmod 644 /usr/syno/etc/php/extension.ini


Now you should be able to open the TinyTiny RSS page by going to http://your-nas.your-domain/tt-rss

To enable regular updates of your feeds:

    
    vi /etc/crontab



    
    */30 * * * * root /bin/su -c "cd /usr/syno/synoman/phpsrc/tt-rss && /usr/bin/php /usr/syno/synoman/phpsrc/tt-rss/update.php --feeds >/dev/null 2>&1" admin


Alternatively, you can start the update process as a daemon:

    
    su -m nobody -c "(trap '' SIGHUP SIGINT SIGQUIT && /usr/bin/php /usr/syno/synoman/phpsrc/tt-rss/update.php --daemon >/tmp/tt.log 2>&1) &"


You will need to restart it manually, if it ever should crash. (Hat tip to [feader](http://tt-rss.org/forum/viewtopic.php?t=1510&p=6785#p6785))

Let me know, if I missed anything...

Helpful articles:



	
  * [http://www.synology-wiki.de/index.php/PhpPgAdmin_als_3rd-Party_Applikation](http://www.synology-wiki.de/index.php/PhpPgAdmin_als_3rd-Party_Applikation)

	
  * [http://it.toolbox.com/blogs/unix-sysadmin/openbsd-and-ttrss-28664](http://it.toolbox.com/blogs/unix-sysadmin/openbsd-and-ttrss-28664)

	
  * [http://www.nas-forum.com/forum/topic/33193-installation-de-tiny-tiny-rss-tt-rss-sur-un-ds1511/](http://www.nas-forum.com/forum/topic/33193-installation-de-tiny-tiny-rss-tt-rss-sur-un-ds1511/)

	
  * [http://www.synology-wiki.de/index.php/Installation_von_Tiny_Tiny_RSS/Installationsskript](http://www.synology-wiki.de/index.php/Installation_von_Tiny_Tiny_RSS/Installationsskript)


