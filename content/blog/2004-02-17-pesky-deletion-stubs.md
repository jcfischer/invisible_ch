---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-02-17 09:15:15+00:00
layout: post
link: https://invisible.ch/2004/02/17/pesky-deletion-stubs/
slug: pesky-deletion-stubs
tags: ["blog"]
title: Pesky Deletion Stubs
type: post
wordpress_id: 250
---

I'm watching over a Notes based Faxserver at a client. There is a lot of personel data imported daily from a SQL database. The process has been taking longer and longer and longer, not finishing and occasionally crashing the server.

Babysitting the process, dropping in occasional log messages (something the original developers didn't do) and doing some educated guesses shows me, that the refreshing of a view is taking in excess of 4 hours.

Some searching on Notes.net points to deletion stubs as a possible problem. Now - how to get rid of them?

Enter [Delstubs](https://www.nsftools.com/tools/delstubs.htm) by [Julian's NSFTools.com](https://www.nsftools.com/).

Here's the result from the first run:
`3924920 of 3924920 records searched

3892146 stubs found
Total space used @ 100 bytes per stub = 389214600 bytes`

Time to use the `/r` removal option...

Let's see the performance after this treatment ;-)
