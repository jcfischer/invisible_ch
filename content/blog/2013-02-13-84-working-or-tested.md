---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-02-13 22:01:08+00:00
layout: post
link: http://blog.invisible.ch/2013/02/13/84-working-or-tested/
slug: 84-working-or-tested
tags: ["blog"]
title: 84 - Working or Tested?
type: post
wordpress_id: 12167
---

Every web application needs to do things asynchronously. Be it that messages need to be passed to other parts of the app, or tasks that take a non trivial amount of time (sending an email, calling into another web service). Ideally, you spin these tasks off from the thread that services the web request and count on them being done in good time, without holding up the request.

Until recently we used [Resque](https://github.com/defunkt/resque) for this. Resque is used in large installations and seems to be battle proof - for us however, it turned into quite a bit of pain. (That is the topic for another blog post). We replaced Resque with [RabbitMQ](http://www.rabbitmq.com/) for message passing and [girl_friday](https://github.com/mperham/girl_friday) for sending mails etc. Both choices have turned out to be excellent so far: We are happy with the stability and the ease of use.

However (and I'm sure you have been waiting for this) there is a problem.

Testing. We had quite comprehensive tests for Resque using [resque_spec](https://github.com/mobino/resque_spec). After last weeks hectic, I found time this week to check our failing Cucumber tests (yes - we deploy even when tests are failing - I used to be  a purist, now I'm pragmatic). All the features that expected certain things to be queued in Resque were failing (of course, because there was no more resque ). I tried to get those tests working again with our new infrastructure, but didn't quite succeed yet.

This led to the in-office quip from [@afussen](https://twitter.com/afussen): "Before, we had tested software that didn't work, now we have working software that isn't tested"

This resonated with what I heard yesterday at the [local.ch](http://local.ch) web tuesday meetup, where [@foz](http://twitter.com/foz) spoke about their experience with their move to Rails. He said something similar to: when we have twice the amount of testcode than production code, we spend an enormous amount of time maintaining the test code, instead of writing new features.

As some of you know, I'm  a bit proponent of Test and Behaviour Driven Design. However, I know for sure, that I have spent many many hours getting the tests running, instead of coding new things. I have been questioning what the "ideal" measure of tests is in a large project, and where the point of decreasing return is. I haven't found the correct answers yet (and I'm not sure I ever will), but I will keep on investigating.

What are your experiences? How much or how little do you test?
