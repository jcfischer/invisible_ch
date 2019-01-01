---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-03-28 17:50:09+00:00
layout: post
link: http://blog.invisible.ch/2013/03/28/41-federated-rabbits/
slug: 41-federated-rabbits
tags: ["blog"]
title: 41 - federated rabbits
type: post
wordpress_id: 12764
---

This post has to do with rabbits (in a way) and is therefore the perfect start to a long easter weekend...

I have been investigating [message queues](http://en.wikipedia.org/wiki/Message_queue) in quite a bit detail lately. We have switched away from [Resque](https://github.com/resque/resque) in Mobino a couple of months ago (mostly to problems with the resque processes loosing their connection to the Redis backend) and switched to a simple work queue implementation with [RabbitMQ](http://www.rabbitmq.com/). This has been working rock solid for the last couple of months and we are very happy with that choice).

We are now looking at re-architecting some other parts of Mobino to use message queues (just because they semantically make a lot more sense than the HTTP REST API calls we are using right now) and I have been playing with different bits and pieces of RabbitMQ. One part that is extremely interesting to us, is the federation of multiple RabbitMQ nodes (running on different server, potentially in different data centers). Federation allows a message sent to one server (server A) to appear on other servers (server B, server C)  (depending on how you wire them together) as if that message had originated on Server B or C.

In order to get a better understanding of how this works, I have put together a local installation of three Rabbit nodes, that are federated. I can then send messages to one of them and see them appear on other nodes.

The new (post RabbitMQ 3.0) way of doing federation is wonderful - it moves all configuration of federation to the server. The clients (message producers and consumers) don't have a clue that they are working through federated queues - this is completely transparent to the client code. This should make it easy to build a solution using one RabbitMQ server first, and then scale up to multiple servers without the code being affected by it.

If you are interested in playing with federated rabbits, then check out my Github repository [rabbitmq-federation](https://github.com/jcfischer/rabbitmq-federation).
