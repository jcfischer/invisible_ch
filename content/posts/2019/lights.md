---
title: "Lights"
date: 2019-01-03T22:32:17+01:00
author: "Jens-Christian Fischer"
image: ""
categories: ["musings"]
tags: ["tech", "fadecandy", "led"]
language: en
slug:
type: post
---

My daughter and I have started working on a LED light installation with several hundred LEDs.
We are using the wonderful [Fadecandy](https://www.adafruit.com/product/1689) board by [Adafruit](https:/www.adafruit.com). A couple of weeks ago, she hooked up their [8x8 Matrix](https://www.adafruit.com/product/1487) 
to the Fadecandy and started to explore programming the lights with [Processing](https://processing.org).

But we have bigger plans. I ordered a bunch of LED strips with 50 WS2812 Neopixels spaced out around 10cm
and we started to work on hooking them up with power and data connections today.

{{< figure src="/images/zoe_soldering.jpg" title="Zoë soldering" >}}

Unfortunately, after a lot of fiddly work, when we tried to turn on the first strip, nothing happened. 
Power seems to be OK, the Fadecandy board communicates with the host computer and seems to work, but no
lights turn on. Restoring the old situation (with the 8x8 Matrix) yielded the same, unsatisfying result...

Let's see what the [Adafruit Forum](https://forums.adafruit.com/viewtopic.php?f=47&t=145733) has to offer
in terms of help - maybe the Fadecandy board got zapped somehow.
