---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-03-01 23:04:50+00:00
layout: post
link: https://invisible.ch/2007/03/02/joyent-strongspace-and-my-samba-server/
slug: joyent-strongspace-and-my-samba-server
tags: ["blog"]
title: Joyent, Strongspace and my Samba Server
type: post
wordpress_id: 610
---

![](/files/Joyent-StrongSpace.png)We use [Joyent][1] (affiliate link) for our mail (born out of Textdrive). Last weekend, the Joyfolks [updated][2] the application to a new version (and had  quite a few problems in the process). One of the new features is [Strongspace][3] integration. Strongspace is a secure storage on the Net (accessible through SFTP, SCP and the like) that I have used for [online backups][4] for quite a while.

At first I didn't think much of the integration, but then it dawned on me, that I could sync our companies shared folder (which lives on a Samba server) to Joyent to get access to all our data when not in the office. Turns out, that this is really easy to do:

The company share lives in `/home/samba/company`. I set up a cron job that sync the share every 15 minutes to the Joyent server:

    0,15,30,45 * * * * rsync -azvCL --progress --delete /home/samba/company/ login@company.joyent.net@company.joyent.net:company/

This sync all changes from the Samba server to the Joyent server. Because rsync assumes that there is one master source for syncing, it doesn't really support two-way syncing. Files that are added to the Joyent connector are deleted on the next rsync. I can live with that limitation for the moment.

In order to allow for syncing without passwords, I use ssh keys. My [backup guide][4] has details on how to do that. Because I sync from my server to the Joyent server, I created a key with an empty password and copied it to the `.ssh` directory on the Joyent connector. 

Neat! And Joyent has just become much more usable. Now if they only would fix some of my peeves (like weeks starting on sunday instead of monday and the lack of a 24 hour clock) I'd be really happy.

[1]: https://www.shareasale.com/r.cfm?B=57232&U;=196165&M;=10198
[2]: https://forum.joyent.com/viewtopic.php?id=959&p;=1
[3]: https://www.shareasale.com/r.cfm?B=69507&U;=196165&M;=10198
[4]: /2005/10/06/back-up/



Technorati Tags: [joyent](https://www.technorati.com/tag/joyent), [rsync](https://www.technorati.com/tag/rsync)
