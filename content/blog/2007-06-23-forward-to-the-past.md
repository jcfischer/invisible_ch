---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2007-06-23 06:36:51+00:00
layout: post
link: https://invisible.ch/2007/06/23/forward-to-the-past/
slug: forward-to-the-past
tags: ["blog"]
title: Forward to the past
type: post
wordpress_id: 623
---

[![](files/forward2past.jpg)](/files/OfflineArbeiten.pdf)This post is a follow up and an expansion to my presentation at [rails-konferenz.de][1] on the topic of "offline Rails applications". If you are not interested in lessons from history, technical details about replication etc. feel free to skip this...

The rage these days is twofold: The "Rich Internet Application" (RIA) and the ability to go off-line. There are a number of ways coming up, that promise you, that you can take (rich) web applications offline. A slew of products are coming out (AIR, Google Gears, [Slingshot][2], ...) that are tackling this problem.

### Problems

And a problem it is! And not something that can be hacked together in a couple of weeks work. Because it turns out, that managing data at several locations (central server, local clients) and keeping track of who changed what, when and to manage any resulting conflicts is difficult. Fiendishly difficult. But it necessary to have the capability of going off-line and still getting work done. Actually - that was the way we all worked just a few years ago. Even though connectivity has improved over the years - from 300 baud modems to "always on" cable or dsl connections - there still are enough places, where connectivity is lacking, bad or unreliable. (Like in the train that I'm currently sitting which is speeding with 240 km/h towards Zurich). One solution is to tick your head in the sand, like [DHH did][3] when Slingshot was announced.

However, the problem has been solved already and productised. And not yesterday, but 21 years ago. A product by a small company out of Cambridge, MA. The company was Iris Associates, which later merged into Lotus Development, which in turn merged into IBM. The product, of course, is Lotus Notes. I have been working professionally with Notes for the last 15 years, and even though it has it's warts, the basic functionality - as devised over 20 years ago - works, and it works rather well, thank you. I know of many projects, that relied (and still rely) on Notes ability to handle disconnected usage (Managing the building of a power plant in the middle of nowhere in Asia, anyone?)

Why is then, that today, this technology has to be re-invented? Is it a case of [NIH][4]? Denial of the past? I don't know, but I wonder...

I presented at [rails-konferenz.de][1] today something titled "Work offline - like in the last millennium". I had planned to give an overview on [Joyent Slingshot][2], show a nifty demo of an application turned off-line. Due to various reasons (most of them being paying clients) the time I had planned on preparing this presentation vanished, with the deadline of the actual date on which the presentation was to be held, approaching fast. Of course I hadn't really looked into Slingshot too much, so the last few days were frentic: Putting a demo together, writing the presentation, looking briefly at AIR and Google Gears, oh - and helping some more clients. 

### When the id is not enough

In the world of Rails databases, we have to use simple numeric ids, to identify records in the database. There has been much discussion about this (and there will likely be more discussions about it in the future), but so far, it seems to work quite OK. A lot of applications have been deployed to the wild wild web, and most of them work fabulously well - simple id field or not. But this simple model is breaking down horribly when the real world enters in the form of disconnected use. There is no guarantee, that a given id hasn't been used in another instance of the application (server, other local client). The way that Slingshot is handling this problem currently, is deeply flawed: Basically, before saving a record, a sanitize function is called. The documentation of this function states, that the developer should take care of ensuring globally unique ids. The "how" is left as an exercise to the reader. 

I can only imagine one use case, where there even is a remote chance of this naive approach has a tiny chance of surviving. That being a single-user application that can be taken offline. And that's a far way off from the promise of offline applications.

Next on the list of dubious design choices is the approach to detect new or changed records. Two additional columns "created_at" and "updated_at" are introduced into every table that needs syncing. While a time stamp mechanism is necessary, again this approach has about 24 problems - the different timezones being one part (solvable), and out-of sync clocks between servers and local clients adding another few problems. The chosen implementation just isn't robust.

Let's try to solve one problem at a time: Clearly the numeric id has to go, we need a universal unique identifier. And it turns out, that this actually is pretty simple: [UUIDs][5] have been around for quite some time and solve the - hah - uniqueness problem of id's. No wonder, when an id looks like this: e9638f8c-200c-11dc-a6c3-0016cb8a850e. Of course ActiveRecord needs some love to actually handle UUIDs instead of the simple id's. Luckily this isn't that big a problem. I will present the technical solution to this in a later post. (Many thanks to [Kaspar Schiess][6] for spending an hour with me just before my presentation to hack away at various parts of ActiveRecord and Slingshot).

### Tracking changes

Changes to data can usually happen at any time - and in any copy of the database. The unique ID and the (normalized) timestamp and a version number will give enough information to determine that a specific record has changed. If the change has happened on one copy only, it's easy enough to update the correct row and move on. The case, when two copies are modified between the same sync interval is tough. There is not enough information available to determine, which copy is "the correct" one. Lotus Notes flags this as "replication conflicts" and they need human intervention to be resolved. 

I have some vague ideas on how this could be partially solved in Rails, but those ideas need some more thought before I'm ready to talk about them. Most certainly we need to track more meta-data on each record. Lotus Notes tracks a lot of additional information in each document, I guess, some clues would come from that implementation.

Also, Lotus Notes's task is a lot easier. Notes has no concept of relations. Each document stored in the database is atomic, and has no ties to other data via foreign key relationships. I have the hunch that a general solution for SQL database will pose some additional challenges...

### Tracking deletions

Not as easy as it sounds either... How does a copy of the database decide, what records have been deleted? Currently, Slingshot sends a list of all valid ids down to the client who has to check his copy of the database and remove those entries that aren't in that list. While this solution works for the simple "one master - one slave" case, it will not support arbitrary topologies of synchronizations. More work is needed on this topic too. Notes solves this, by sending so called "deletion stubs" around - basically pointers that tell the receiving database, that a certain document has been deleted. These deletion stubs themselves can travel to other databases. Again, this problem is made more difficult due to the fact of relations in the database...  

### Forward to the past

So where does all of this leave us? Are the off-line database/web applications doomed from the start? I don't think so. I have a feeling, that quite a few general cases of "everybody can change all data" can be specialized to a much more restrictive model. And restrictions are good in this case, because they take away complexity. I think that we can come up with solutions that will handle 80% of the necessary work - and with careful design of the applications, we can make the other 20% go away. I'm optimistic about off-line (rails) applications and will likely spend some more time on these problems. (Or maybe, the next release of Slingshot has all of this solved already. Yes, I'm an eternal optimist)

The [slides of my presentation][7] are available online. A video of the presentation is forthcoming.


[1]: https://www.rails-konferenz.de
[2]: https://www.joyent.com/slingshot
[3]: https://www.37signals.com/svn/posts/347-youre-not-on-a-fucking-plane-and-if-you-are-it-doesnt-matter
[4]: https://en.wikipedia.org/wiki/Not_Invented_Here
[5]: https://en.wikipedia.org/wiki/Uuid
[6]: https://neotrivium.com/blog/2006/12/4/autor_kaspar_schiess?img_pos=2
[7]: /files/OfflineArbeiten.pdf


Technorati Tags: [domino](https://www.technorati.com/tag/domino), [joyent](https://www.technorati.com/tag/joyent), [lotus notes](https://www.technorati.com/tag/lotus notes), [ozzie](https://www.technorati.com/tag/ozzie), [uuid](https://www.technorati.com/tag/uuid), [rails-konferenz](https://www.technorati.com/tag/rails-konferenz), [replication](https://www.technorati.com/tag/replication), [slingshot](https://www.technorati.com/tag/slingshot)
