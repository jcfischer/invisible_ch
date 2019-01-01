---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-08-29 21:40:18+00:00
layout: post
link: http://blog.invisible.ch/2004/08/29/internal-yes-extneral-no/
slug: internal-yes-extneral-no
tags: ["blog"]
title: Internal YES, extneral NO
type: post
wordpress_id: 313
---

I have struggled to install Debian on my [new file server](/archives/000311.html). With the new installer disk this was a breeze - until it tried to download additional packages from the internet. Turns out that I had access to my internal network, but no access at all to the external world.

I checked the things one checks in this situation: ifconfig: OK, /etc/network/interfaces (OK - and I tried both DHCP and static), route -n (route to the internal network and to the ADSL router as gateway: OK), /etc/resolv.conf (had the DNS servers of my provider, but I couldn't ping them), IPCHAINS - emtpy table), network cable (changed several times), router ports (plugged it in into one port that I know worked)

Nada. Nothing. Installed the 2.4 kernel instead of the 2.6

Booted with an old Knoppix CD: Nothing

Is it possible that a network card only connects to an internal network? Am I going mad?

This is the internal network card of an Dell PowerEdge 1400 SC.

HELP!
