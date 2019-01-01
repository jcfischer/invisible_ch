---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-05-10 10:32:07+00:00
layout: post
link: http://invisible.ch/2004/05/10/most-stupid-url/
slug: most-stupid-url
tags: ["blog"]
title: Most stupid URL
type: post
wordpress_id: 272
---

Having clear URLs on your page or in your web applictation not only is a help to users, but make you think about structure and usability. And - [I was wrong](/archives/000132.html)

I just happend to come across an email on the [Prius Mailing List](http://de.groups.yahoo.com/group/toyota_prius_de/) that had a number of links to Prius ressources.

With great pleasure I present to you the most outraegous URL I have ever come across (and as a Domino Developer, I have come across nasty URLs, believe me!)

[http://www.tagblatt.ch/interessen.cfm?pass_id=904446&liste;=905193,905191,905190,905156,904970,  
904532,904531,904530,904529,904528,904527,904458,904457,  
904456,904446,904445,904443,904442,904441,904156,904155,  
904153,904113,904111,904110,903668,903667,903666,903665,  
903623,903553,903429,903428,903427,903426,903214,903212,  
903174,902975,902974,902973,902972,902547,902546,902545](http://www.tagblatt.ch/interessen.cfm?pass_id=904446&liste=905193,905191,905190,905156,904970,904532,904531,904530,904529,904528,904527,904458,904457,904456,904446,904445,904443,904442,904441,904156,904155,904153,904113,904111,904110,903668,903667,903666,903665,903623,903553,903429,903428,903427,903426,903214,903212,903174,902975,902974,902973,902972,902547,902546,902545)

What's this articla about? Who programmed this CMS? What were they thinking?

While developing [ZAPPATA](http://www.zappatanetworks.com/) we have spent countless hours on making the URLs of ZAPPATA it's [UI](http://www.useit.com/alertbox/990321.html) (yes - it is browser based, another nugget of information to all of you waiting for more details) easy, understandable and hackable. Looking at our URL structure, I think we are doing OK - and in light of the above example, I think we are actually doing great...

Devising systematic URLs is a) non-trivial and b) a lot of work. But the months spent on ZAPPATA have made me painfully aware of how important that "little detail" in web site design is. While I don't know if the "average user" will notice that site structure and it's representation in the URL are consistent, the effect this work has, will be felt by the user. It's easy to add features, sections, functions to a website or a web application. Thinking about how these features can be adressed with URLs will in my opinion lead to a better designed and more usable website.

In my earlier web applications I tried to overcome the browsers limitations as much as I could. Display web based dialog boxes, hide browser buttons, track state of a transaction. The results were never quite satisfying. Due to the used technology (Domino) my URL's were a mess (think two 32 character long universal ID's in the URL) and the logic (both server and client side) to keep track of state was a nightmare. 

But it makes so much more sense to recognize that the browser is -- hold it -- a browser, and not a sophisticated fat client with tons of functionality. Once that realisation sets it, the challenge become to desing an application that doesn't try to mimic a rich UI (and there are some amazin examples out there 

ZAPPATA uses a pure URL based interface. Everything can be adressed with a URL. Neither server nor client keep state. Everything is bookmarkable (searches, actions, lists). I have seen the light and [retract what I said earlier](/archives/000132.html).

If your application runs in a browser, make sure it works well in the browser and looks and feels like a well designed web site.
