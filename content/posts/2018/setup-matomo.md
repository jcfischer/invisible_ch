---
title: "Setup Matomo"
date: 2018-12-31T21:58:55+01:00
author: "Jens-Christian Fischer"
description: "Setting up a Matomo Server"
image: ""
categories: ["code"]
tags: ["tech"]
language: en
slug:
type: post
---

I like Analytics on a website, I don't want to use Google Analytics. That leaves
me with only a few options, one it to run my own analytics software somewhere I control.
Previously I used Piwik with good success, so it seems sensible to set that up. Piwik
has been renamed to [Matomo](https://matomo.org) and I haven't found a simple complete
installer.

## Server Setup

I know that I should use something like Ansible to set it up, but I'm doing it by hand for 
now.

Based on these instructions [Install LEMP Stack](https://linuxconfig.org/how-to-install-nginx-mariadb-php-lemp-stack-on-ubuntu-18-04-bionic-beaver-linux), 
[Install Matomo](https://linuxconfig.org/how-to-install-matomo-open-source-analytics-on-ubuntu-18-04-bionic-beaver-linux)
and [Nginx and Letsencrypt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-18-04)
here's what I did on a fresh Ubuntu Bionic VM:

    $ sudo apt-get update && sudo apt-get upgrade
    $ sudo apt install mariadb-server nginx php-fpm php-mysql php-mbstring php-dom php-xml unzip
    $ sudo systemctl start php7.2-fpm
    $ sudo systemctl enable php7.2-fpm
    $ sudo add-apt-repository ppa:certbot/certbot
    $ sudo apt install python-certbot-nginx
    $ sudo mysql -u root
    mysql> CREATE DATABASE matomo;
    mysql> CREATE USER `matomo_admin`@`localhost` IDENTIFIED BY 'verysecret';
    mysql> GRANT ALL ON matomo.* TO `matomo_admin`@`localhost`;
    mysql> FLUSH PRIVILEGES;
    ^D
    $ wget https://builds.matomo.org/piwik.zip
    $ unzip piwik.zip
    $ sudo cp -r piwik /var/www/
    $ sudo chown -R www-data:www-data /var/www/piwik
    $ sudo touch /etc/nginx/sites-available/ch.invisible.matomo
   
    
Then edit the newly created file
   
    server {
            listen 80;
            listen [::]:80;
            server_name matomo.invisible.ch;
    
            index index.php;
            root /var/www/piwik;
    
            access_log /var/log/nginx/ch.invisible.matomo.access_log;
            error_log /var/log/nginx/ch.invisible.matomo.error_log;
    
            location / {
                    try_files $uri $uri/ =404;
            }
    
            location ~ \.php$ {
                    include snippets/fastcgi-php.conf;
                    fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
            }
    }
    
Get a certificate and enable the site:

    $ sudo certbot --nginx -d matomo.invisible.ch
    $ sudo ln -s /etc/nginx/sites-available/ch.invisible.matomo /etc/nginx/sites-enabled/ch.invisible.matomo
    $ sudo rm /etc/nging/sites-enabled/default
    $ sudo systemctl restart nginx    

Enter the DNS entries for the server, and it should start responding. Go through the setup
wizard, enter `matomo_admin` for DB user, `matomo` for DB name, the `verysecret` password, remove
the 'Table Prefix'. The rest of the wizard should be self explanatory.

## Hugo Setup

To enable Matomo Tracking, use [hugo-component-matomo](https://github.com/holehan/hugo-component-matomo). You
will also need to enable the `AjaxOptOut` Plugin in Matomo. (Settings -> Plugins)

