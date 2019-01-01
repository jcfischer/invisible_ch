---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-07-26 21:57:10+00:00
layout: post
link: http://invisible.ch/2005/07/26/lotus-domino-server-with-odbc-connection/
slug: lotus-domino-server-with-odbc-connection
tags: ["blog"]
title: Lotus Domino Server with ODBC connection
type: post
wordpress_id: 438
---


On one of my customer projects, I needed to access an Oracle 9 database to transfer information from a Notes database to the SQL database. Because this was going to be an intermediate solution, only for a couple of weeks, I hacked together something that used the Oracle ODBC driver and installed it at the customers site.



We got it to work on a R6 Notes client, but not -- as intended -- on the R5 server they had hidden away in some basement. Recently we moved to another Notes server (R6.5 this time) but the agent still had problems.



Here's my findings:




  * The ODBC driver brings up a login dialog box, if it can't access the database (which is an absolutely brilliant thing to have on server)


  * The very same agent in the very same database was running on a R6.5 client on the server, but not on the R6.5 server. Of course, both the client and the server were on the same physical machine.


  * The server was running as a service, and only when I set the server to run under my account (and not the system account), it would connect using ODBC. 




Now that we had the server talking ODBC it even seemed to work. I set the agent to run every 15 minutes. And run it did - periodically. For about 2 days. Then the Agent Manager was frozen and only liberal use of "killnotes.exe" brought it down.



Because the intermediate solution is going to last for at least another six months, I'm going to rewrite the agent, using the Lotus Oracle Connectors. Joy. And to do that, I have to install the backlevel Oracle 8 tools on the server. More Joy. 



Hopefully this text helps somebody against deciding to use Notes and ODBC drivers...





Technorati Tags: [lotus notes](http://technorati.com/tag/lotus notes), [domino](http://technorati.com/tag/domino), [odbc](http://technorati.com/tag/odbc)
