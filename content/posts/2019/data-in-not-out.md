---
title: "Data in, Not Out"
date: 2019-01-05T16:04:48+01:00
author: "Jens-Christian Fischer"
description: ""
image: ""
categories: ["musings"]
tags: ["tech", "led", "fadecandy"]
language: en
slug:
type: post
---

While we didn't have much success [a couple of days ago](/2019/01/lights/), today we got the lights to
work properly. Turns out, that I've made the beginner mistake number 1 when dealing with [Neopixels](https://www.adafruit.com/category/168) &mdash; 
I connected the data signal from the Fadecandy to the DOUT pin of the LED strip (there's also a DIN pin, at the
other end of the strip). The "D" stands for "Data", while I will leave you to guess what OUT and IN mean... To make
this work, the data needs to go to the DIN port of a pixel strip...

I should have read the [Digital LED Strip Read Me First](https://forums.adafruit.com/viewtopic.php?f=47&t=24847) first.

A view of the completed electronic mess with a bonus of a deeply sceptic cat:

{{< youtube FGBd9_B0taU >}}


