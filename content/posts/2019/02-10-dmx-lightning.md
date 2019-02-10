---
title: "DMX Lightning"
date: 2019-02-10T19:14:14+01:00
author: "Jens-Christian Fischer"
description: "Choosing the right software make for a flicker free experience"
image: "/images/2019-02-10-lightkey.jpg"
categories: [ "tech"]
tags: ["dmx", "light"]
language: en
type: post
---

Last year I bought some cheap DMX capable lights - a [Full Color Brick](https://www.thomannmusic.ch/stairville_xbrick_fullcolour_16x3w.htm) and a 
[Mini White Par](https://www.thomannmusic.ch/stairville_mini_stage_par_cw_ww_a.htm). Both work fine without any additional
contols - the Color Brick can fade through various colors and the Par can be set to a specific white value.

It is clear, that this is not enough, so I got a cheap [USB to DMX](https://www.aliexpress.com/item/Android-Mac-win8-win10-with-xlr-3p-female-ftdi-usb-rs485-dmx-cable-for-Stage-Lighting/32789287966.html)
interface to control the two lights and start out in Light Show Business. Also, there needs to be software. A quick search for DMX software turned
up [QLC+](https://www.qlcplus.org/) - a free, cross plattform, open-source software. What's not to like?

Well, the user interface for starters. 

{{< figure src="/images/2019-02-10-qlc_plus.png" caption="The sheer beauty of the QLC+ QT UI" >}}

But the UI is only part of the game. Functionality wise, QLC+ has a lot to offer, and after a couple of hours
I had various blinking, color-fading lights, controlled by a MIDI controller up and running. 

There was only a small problem: The lights flickered. Randomly. They seemd to turn off for a fraction of a second
in random intervals - every couple of seconds. I blamed the cheap DMX interface and started to research
some more professional (and much more expensive) options.

Then I paused with the whole lighting setup and concentrated on practicing guitar again.

This afternoon, while taking a break from learning a jazzy, Bossa Nova version of [Sunny by Sandra Sherman](https://www.youtube.com/watch?v=JenuxAXNrdw) 
(who is a wonderful Youtube guitar teacher), I thought about trying out other software. Another search led me to find 
[Lightkey](https://lightkeyapp.com/en/), a Mac only, commercial (gasp) software. It seemed to support my DMX adapter
so I installed it. The difference in UI was staggering - a beautiful, Mac like UI. Setting up a scene was a breeze and it
even detected my USB adapter.

The only problem: It didn't work. The lights basically went on or off at random (if at all) and there didn't seem to be any
method to the madness. I researched their knowledge-base and the internet, downloaded specific drivers for the FT232 chipset, 
rebooted a couple of times and had no luck. While installing, I got a message that Lightkey was trying to install OSX Kernel
extensions. I thought I had allowed that, but it turned out that that didn't stick. Enabling the KExt, rebooting and starting
Lightkey again, it detected the correct version of the hardware (it had selected another USB DMX adapter, the Eurolite USB DMX).

And now - hey presto: Everything worked, the lights didn't flicker and I was able to re-use and adapt a number of nice
effects.


{{< figure src="/images/2019-02-10-lightkey.jpg" caption="The Lighkey UI is beautyful" >}}

As for the price? There's a free version that supports only 24 DMX channels. Currently, I use 17, so I'm all good. After that, prices 
start at USD 69 / year for 256 channels. While not cheap, the software looks great, easy to use and seems to be worth it. We'll 
see as I get more lights to control.



