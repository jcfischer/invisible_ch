---
title: "Travis checks Chaschper"
date: 2019-01-14T17:51:33+01:00
author: "Jens-Christian Fischer"
description: "Updated hugo-chaschper theme with CI tests"
image: "/images/TravisCI-Mascot.png"
categories: ["code"]
tags: ["tech", "hugo", "travis"]
language: en
slug:
type: post
---

One of these "ohh - that's a nice idea, I should totally also implement that" ideas. I stumbled upon the
[Dream Plus](https://github.com/UtkarshVerma/hugo-dream-plus) Hugo theme, that included a little badge
that linked to a [Travis CI](https://travis-ci.org/UtkarshVerma/hugo-dream-plus) build status. 

Using CI (Continous Integration) to check the sanity of the template seemed like a good thing to me, so I looked
around on how various people do this. I found [one template by Vicky Lai](https://github.com/vickylai/hugo-theme-sam) that included HTML checking. After a bit of fiddling around, to get the correct command line incantations going, and some
more fixing of malformed HTML, the [Hugo Chaschper](https://github.com/jcfischer/hugo-chaschper) template now
is tested, the `exampleSite` is updated to include some "real" content and a number of niggling issues in the
HTML have been fixed (missig `alt` image attributes, a malformed `<script</script>` tag).

Current build status of the theme: [![Build Status](https://travis-ci.org/jcfischer/hugo-chaschper.svg?branch=master)](https://travis-ci.org/jcfischer/hugo-chaschper)

The HTML proofing is done via the [HTML-Proofer](https://github.com/gjtorikian/html-proofer) Gem. It checks
for valid HTML, valid (internal) links and a lot more. 
