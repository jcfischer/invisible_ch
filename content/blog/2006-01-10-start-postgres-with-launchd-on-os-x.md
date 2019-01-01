---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2006-01-10 10:27:41+00:00
layout: post
link: http://invisible.ch/2006/01/10/start-postgres-with-launchd-on-os-x/
slug: start-postgres-with-launchd-on-os-x
tags: ["blog"]
title: Start postgres with launchd on OS X
type: post
wordpress_id: 501
---

The startup item for Postgres on OS X always fails on Tiger. Launchd (the launch daemon) to rescue:

[PostgreSQL launchd on Tiger][1] gave me the starting point and my /Library/LaunchDaemons/org.postgresql.PostgreSQL.plist looks like this:

    < ?xml version="1.0" encoding="UTF-8"?>
    < !DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    
    
	    GroupName
        postgres
        Label
        org.postgresql.PostgreSQL
        OnDemand
        
        ProgramArguments
        
            /opt/local/lib/pgsql8/bin/pg_ctl
            -D
            /opt/local/var/pgsql8/defaultd
            -l
            /opt/local/var/log/psql8/
            start
        
        RunAtLoad
        
        ServiceDescription
        PostgreSQL Server
        UserName
        postgres8
    
    



[1]: http://openacs.org/blog/one-entry?entry_id=296430


Technorati Tags: [mac](http://www.technorati.com/tag/mac), [postgresql](http://www.technorati.com/tag/postgresql), [launchd](http://www.technorati.com/tag/launchd)
