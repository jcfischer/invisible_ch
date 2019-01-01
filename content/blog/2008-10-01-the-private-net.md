---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2008-10-01 20:28:49+00:00
layout: post
link: http://invisible.ch/2008/10/01/the-private-net/
slug: the-private-net
tags: ["blog"]
title: the private net
type: post
wordpress_id: 691
---

This article has been gestating in my mind for quite some time. It was pushed
closer to being written by an incident a couple of weeks ago. I run a number of
different websites (in this context namely [iphone-essentials.ch][1]). Also, since
a couple of years, I had a Google AdSense account and ran ads, not to cover my costs 
(the payouts were too low anyway) but as matter of getting a feel for this method
of monetization on the web. To make a long story short: It doesn't work! A reasonable
successful website (500 - 1000 unique users per day, on iphone-essentials.ch) brings
in 1 to 3 USD in AdSense commisions per day. In my experience AdSense earnings scale
very linearly with number of visitors, so I could have made maybe 20 USD if I had
10'000 uniques per day.

But I can't. Not because I don't have the visitors (I don't), but because Google has
decided that I'm a threat to their AdWords advertisers. How they arrived at this conclusion
is a mystery to me: Google doesn't explain what was wrong. They just cancelled my
account, kept the balance of 160 USD that wasn't yet paid to me and basically told me to
f*** off.

With that introduction (which also might give you a hint of the bias I might have) onwards
to the rest of the article.

The other gestation point is the upcoming [Web 2.0 Expo in Berlin][9]. I will be attending as
part of the blogging programme. I will try to see, if the things I describe in this
post are at all a part of the discussion.

I love Google. I have been using their search engine ever since I saw it the first time. Their
web apps are pure joy. Goggle Maps, Google Mail, Google Docs: Wonders of usability and good
value. I had seriously contemplated moving our complete mail infrastructure to Google Apps, for
a very reasonable 60USD/user/year. I had started on using the collaboration features in Google
Docs, writing, computing, sharing and collaboration on internal documents, and documents for 
clients. 
Google Chrome looks like a beautiful, speedy, reduce-to-the-max web browser and the few tests
I made with it show great potential.

But this action of Google, cancelling my account with them, has changed that. We have all heard
the discussions about Google and privacy. Anybody web savvy knows, that there ultimately is
no privacy to be had on the internet. Too many traces are left on our trails through the vast 
web space. Government agencies are routinely listening in on communications, ISPs are required to
keep track of all logins and all email communication, Google wants to know who you are and what
you read to optimize the ads they are serving to you. 

Enough! While we can't erase all traces of our online lives, we can take care to not leave too
much in this Web 2.0.

As an individual, or a small company, I have some limited possibilities. Each one does not amount to
much, but together they make me and my employees less transparent, less open to snooping and 
give us back a bit of the privacy that I think we are entitled to.

And yes: This comes at a price... Both financially and in terms of ease of use. This price I am 
willing to pay.

EMail
-----

We used to host our companies EMail at [Joyent][2], a hosting company that I have used (and will 
continue to use) for many years. Additionally, I had a number of GMail accounts (for mailing lists,
for sites where I didn't want to divulge my real email, etc.).
Our companies EMail was moved to [Zimbra][3], hosted on my own server, in a data center down the
street. Zimbra has a lot of features, email, calendaring, collaboration, iPhone integration etc. 
It's fairly easy to set up, and has been performing well so far. The big advantage over Joyent? My 
data is hosted in Switzerland, under swiss jurisdiction. While I trust Joyent and the people behind 
Joyent, my data could still be seized by a court order. While this is far fetched in our companies case,
large companies that move their mail to someone based in the US (like Google) might find all their
private EMails subpoenaed by a US court.
I'm divesting my Google mail accounts too, moving them, depending on need, to other free mail providers 
(like Yahoo) or my own server.
The cost? The server costs, the co-location costs, Zimbra costs, setting it up costs. We are planning
on divesting some of the cost, by offering hosted Zimbra to our customers. If you are interested
in an email provider in Switzerland, give me a holler, and you can get a ride on my box.
The benefits? My email is completely under my control. We get better and more features than previously
(company calendaring, iPhone integration, great web UI)

Search
------

It's almost impossible to be better than Google. MS Live Search and Yahoo search account for 
almost no traffic to a website (as any web master will tell you). New companies (like [Cuil][4]) sometimes
make a big splash, but have little impact.
Still, search is probably the most important application on the web. What to do? A project named [YaCy][5]
is building a distributed, peer to peer, anonymous search engine. It is fledgling, indexes around 600 million
web pages (depends on how many peers are online at any given moment), has a UI that could be improved 
quite a bit, needs a lot more work on getting search results as good as Googles (the PageRank algorithm
really does make a difference!) and the software is in development.
But the search is anonymous, the ranking algorithms are public, there is a way to help the search engine
make better decisions.
I have started to run a 24/7 peer in the YaCy network. So far it has crawled a bit over 2 million pages
and thus contributes a tiny part to the web known to YaCy. I have set it up so that it tries to capture
areas of the web that interest me: Rails, Ruby, Smalltalk. Also YaCy acts as proxy to my web browser
and sees every page I read and uses that to expand the areas of the web it's crawling.
I have no illusion of YaCy being as good as Google any time soon. But I find it important to start to
try to break the dominance of the 700 pound gorilla. My peer is open: [search.invisible.ch][6], feel free
to come by for your search needs. 
The cost? The server and the bandwidth (which I already pay for for our email). Not as good search
results as the ones provided by Google.
The benefits? Helping an important project. Giving less information to Google.

Network
-------

The IP based network is here to stay, and little can be made of changing the infrastructure. However, the
infrastructure can be 'used' in a slightly different way to thwart eavesdropping etc. An interesting 
project is [Freenet][7] which basically is a content-delivery darknet. It's goal is to distribute information
in a way, that the information can't be censored, deleted and that participating nodes have no idea
and no way of knowing, what content is stored and delivered on their servers. In addition, the servers
themselves are stealthy: it's not easy to detect them. I ran a Freenet node a couple of years ago and 
have donated to the project. However I have stopped, because I had no immediate use case for it. The available
content (if you could get access to it) was of questionable or legally problematic nature. While the goals
of Freenet are noble, and the technology is interesting, I don't think it's a viable solution for general use.

Of more interest to me is [TOR][8]. TOR consists of a series of servers, that route IP traffic in a 
non-traceable way. It's not possible to tell for an eavesdropper, which websites I looked at, and the 
websites have no way to know, who I am based on my IP address. The TOR network is based on a large number
of TOR servers, and users proxying through them. There are a few problems: even though the TOR net gives
anonymity, it does not give you security, as the recent case of 'hacked' embassy email passwords showed. A
'poisoned' exit-node (the last server in a chain of servers, that contacts the intended destination server)
was logging all mail related traffic and was able to extract hundreds of passwords. 

If one runs an exit node, large amount of 'inappropriate' trafic (spam, if you allow mail) originates from your
server: a sure way to get your IP listed on a blacklist. 

I have been thinking of running a TOR node on my co-located server, and force all trafic from my office through
it, but I'm not quite sure about the implications yet. One concern is speed: the routing of all traffic through
multiple servers takes time and is limited by the bandwidth of the slowest link. 

EMail, take2
------------

There is yet another problem with EMail: It get's transfered throug ISPs on the way and can be intercepted
and read. Encryption of EMail is possible (PGP, S/MIME) but non standard and few people use it. A couple
of years ago, I worked with 2 friends on [Zappata][8] which evolved over time into a secure P2P email system.
We had a proof of concept working, could send and receive email, had built a PKI infrastructure that allowed
authentication and encryption but in the end, the project fell apart because of lack of funding.
I still think that the idea behind it is viable, and I would love to resurrect it: if you happen to have
around USD 100'000, a strong interest in wide spread encryption, give me a shout - we could bring the 
project back to life and deliver a working solution within a few months.

Conclusion
----------

While the net, and the web, are inherently insecure and traceable and there are strong corporate interests
in collecting as much information about you as possible, there are ways to take back some control - at 
a cost. It's up to the individual or the corporations to decide how much value they place on control
over their data, their usage patterns, and how much they are willing to cede to get things free.

Me and my company have made the decision to 'pay the price' and start to become independent of the sweet
smelling and looking offers from corporations like Google. I would hope, that more people will follow.



[1]: http://iphone-essentials.ch
[2]: http://joyent.com
[3]: http://zimbra.com
[4]: http://cuil.com
[5]: http://yacy.net
[6]: http://77.95.121.149:8080
[7]: http://freenetproject.org
[8]: http://www.zappatanetworks.com
[9]: http://en.oreilly.com/webexberlin2008/public/content/home
