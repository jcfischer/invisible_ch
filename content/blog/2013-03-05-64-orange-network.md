---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2013-03-05 22:14:14+00:00
layout: post
link: http://blog.invisible.ch/2013/03/05/64-orange-network/
slug: 64-orange-network
tags: ["blog"]
title: 64 - orange network
type: post
wordpress_id: 12620
---

Today I was [invited to a friendly talk with two Orange network engineer](http://blog-orangech.com/2013/01/17/orange-ladt-euch-zu-einer-netz-diskussion-ein/)s to talk about - tada - the Orange Cellular network in Switzerland. [@Stephtara](http://climbtothestars.org/) had facilitated this meetup for bloggers and members of the Orange community and Orange brought in two engineers that are working on the actual network. In a really interesting roundtable discussion, we were able to fire off lots of (technical) questions about cellular networks in general and the Orange network in particular.

We had interesting 90 minutes and I personally learnt loads about the cellular networks in Switzerland.

I was too engulfed to take notes (I'm sure my colleagues did better, and I will link to them when and if they have posted something), but here are some of the take aways I remember:



	
  * Orange has spent a lot of energy bringing up their network to speed (literally). There lack of 3G coverage was one of the reasons I left them 2 years ago.

	
  * Building and maintaing a cellular network is an intricate balance of money, technical issues, political issues - it's not really easy to just prop up a new cell tower to improve performance

	
  * Switzerland has extremely strict radiation laws, in fact the biggest problem of all cellular carriers in Switzerland is the amount of radio power that is allowed at any given point. It is 6V/m while other European countries allow up to 41V/m. The crux (for the cellular operators is, that 6V/m is the sum of all radiation power of all providers). So if there are 2 cell towers operating, a third one can't raise the radiation level (which means that the others would have to transmit less power)

	
  * Orange is starting with 4G (LTE) in June, in 10 cities in Switzerland

	
  * This is relatively easy for them, as they can upgrade their 1800MHz, 3G towers (although they have to reduce the power of the 2G, 3G emissions on those towers - see above)

	
  * Cell towers get regular software updates, that increase the data capacity (voice capacity is relatively fixed)

	
  * Voice is still growing, while data usage is exploding in comparison

	
  * 4G is much, much better for data than 3G (which has a number of problems - namely initial latency to create a TCP/IP connection of up to 3 seconds)

	
  * Current 4g phones drop down to 3G when a voice call comes in, resulting in a noticeable hick-up in data transfers. Next years generation of phones will be able to keep both a 3G voice, and a 4G data connection at the same time

	
  * Voice calls will go VoLTE (Voice over LTE) in the near future, this will allow the carriers to do QoS (Quality of Service) for those voice calls. Currently, Orange doesn't do any traffic shaping on their data networks. VoIP can work very well - unless you are in cell with a lot of other people using data

	
  * New cheap phones are starting to use 3G chipsets instead of 2G ones. This will allow the carriers to phase out 2G sometime in the future (2G is inefficient to operate, requires too much power - see above)

	
  * The future in highly dense areas are smaller cells, with cell towers with lower radiation energy, going all the way down to femto cells. (A femto cell is like a private cell tower that you plug into a home DSL. It has a range of maybe 20 meters, similar to WiFi)

	
  * Carriers have a lot of control over how their cells are utilized (this in response to my question why I often get 2G reception in Zurich on Sunrise. They Orange people of course don't know why Sunrise is behaving like this - they said, that the towers employ a lot of different strategies to fulfill requests). Orange tries to keep as much traffic on 3G as possible.

	
  * Repeaters in trains for cellular reception are shared between the 3 carriers - and they take a lot abuse (vibrations, dust) and can only be serviced every couple of months (with the service schedule of the train)

	
  * probably more that I forgot...


All in all a very interesting talk, with a lot of highly detailed answers from the two engineers that were there. A lot of the problems that we are having with cellular reception in Switzerland are the function of physics coupled with very strict laws, and nothing that can just be solved easily.

It was great to hear from "the horses mouth". Hearing an engineer talk about the problems and difficulties they are facing, and how they are solving them, beats any marketing speak.

Thanks to Orange for hosting this, and for giving us access to this kind of information. Extremely interesting and highly appreciated.

As I have quit Sunrise (I'm now ex-Swisscom, ex-Orange and soon ex-Sunrise) I need to find a new cellular carrier (i.e. one of the three I already left) in August....
