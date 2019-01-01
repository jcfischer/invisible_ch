---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-09-29 23:21:08+00:00
layout: post
link: http://invisible.ch/2004/09/29/new-beta-of-zappata-released/
slug: new-beta-of-zappata-released
tags: ["blog"]
title: New Beta of ZAPPATA released
type: post
wordpress_id: 328
---

We have released a new build of [ZAPPATA](http://www.zappatanetworks.com) today. You can grab it from the [Download](http://www.zappatanetworks.com/download) page.

We spent a lot of time polishing the IMAP server and it should behave nicer with a wider variety of clients.

The [IMAP RFC 3501](http://www.faqs.org/rfcs/rfc3501.html) is not exactly lightweight, and the protocol is very powerful and very chatty. There are a lot of things that can go wrong in IMAP transactions between email clients and servers. It's been interesting to see how different clients talk to the server. Each client I have observed (Outlook & Outlook Express, Opera, Thunderbird, The Bat!, Mulberry) handle the task in a different way. Demanding.

Let me know, if it works for you and your specific email client.
