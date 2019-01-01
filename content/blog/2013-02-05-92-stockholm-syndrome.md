---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-02-05 23:17:28+00:00
layout: post
link: https://invisible.ch/2013/02/06/92-stockholm-syndrome/
slug: 92-stockholm-syndrome
tags: ["blog"]
title: 92 - Stockholm Syndrome
type: post
wordpress_id: 12139
---

The [Stockholm Syndrome ](https://en.wikipedia.org/wiki/Stockholm_syndrome)is described as when hostages evolve sympathy or empathy with their captors.

That's what I felt yesterday evening, hours before an email went out to 1000 participants of the [Lift Conference](https://liftconference.com) in Geneva where we are showcasing [Mobino as the official mobile payment provider](https://liftconference.com/news/2013/02/03/private-launch-mobino-mobile-payment-solution-lift13) - and we found a critical bug in our iOS app that was sent to review to Apple a good week before.

If all goes well, Apple currently takes around 6 days to review and approve an application for the iOS AppStore. We counted on being reviewed and approved yesterday evening, with another day to spare (the conference starts tomorrow). Worst case, we still had the old version in the AppStore that was missing one noteable feature, but still was fully functional and usable. Then however, one of our customer found a problem. And it turned out, that this problem was much much bigger than it first seemed like. In effect, it would have prevented everybody with an iPhone set to regional settings that use a comma for decimal separation to crash. And two countries that have this are France and Germany. Not good. Especially because the crash happened in the version that was available and the one that was in review.

We investigated if it would be possible to fix the issue by sending data in a different format from the servers, however that was not possible. The app itself had a serious bug in the treatment of numbers based on the locale. Fixing this took around 45 minutes. We found some people in Germany to test the fix and confirm it was working in the wild.

That left us with Apple. Submitting a new binary while waiting in the review queue  resets your place in the queue, putting you back at square one. Not an option in our case. Luckily, Apple has the "expedited review request form" that you can fill out and state your urgent need. So we did, and - amazingly enough - got a reply within 2 hours (not usual). The moaned about us already having used an expedite request in the past, but still granted it.

This is where I felt happy: Stockholm Syndrome kicking in. We don't have those problems with our Android app. We discover a bug, we fix it, we publish the app into the PlayStore. Done, delivered.

With Apple, making a release is a major undertaking that needs extremely good timing. (And of course, a number of things went wrong with this urgent release - some things don't work as they should - we just didn't do the full QA because of the time pressure we had yesterday. Still - the App works well enough and we are taking our time to fix the remaining problems before submitting it again)

The real kicker though is the review. It took all of 2 minutes from the moment the reviewer started the app until it was approved. (And most of that time was spent in the registration process)

I love Apple, I love their products (although that has declined the last years - but that is the topic for another post). Their App Store policies are difficult at best to live with as a software developer. Still interesting to see, how happy a granted "expedite request" can make me...
