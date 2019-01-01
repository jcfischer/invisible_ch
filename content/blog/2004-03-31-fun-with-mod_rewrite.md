---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-03-31 14:01:31+00:00
layout: post
link: https://invisible.ch/2004/03/31/fun-with-mod_rewrite/
slug: fun-with-mod_rewrite
tags: ["blog"]
title: Fun with mod_rewrite
type: post
wordpress_id: 261
---

I don't like people deep-linking to my images. And neither do others. Some quick mod_rewrite rules helps...

I noticed an increased activity on my blog and a lot of referres from an italian site recently. Today I had time to look at the logs and I found a site that linked to my Gicaometti image.

I didn't like that too much, so I googled a bit and found [ChaosReigns cure](https://www.chaosreigns.com/adventures/entry.php?date=2001-11-28&num=01). He excluded everybody from deep linking, but I only wanted to make the point to this one person.

After some experiments with mod_rewrite, here's my newest inclusion in httpd.conf:

`
RewriteEngine On
RewriteLog /var/log/httpd/rewrite.log
RewriteLogLevel 7

RewriteCond %{HTTP_REFERER} ^https://.*splinder\.it/.*$
RewriteCond %{REQUEST_URI} !^/bad.jpg$ [NC]
RewriteRule .*\.(gif|jpg|png|bmp)$ /bad.jpg [NC,R,L] 
`

Of course bad.jpg looks really nasty ;-) (and I stole it shamelessly from Chaos Reigns. At least I copied it to my server first ;-)
