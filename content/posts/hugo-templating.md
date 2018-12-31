---
title: "Hugo Templating"
date: 2018-12-31T13:38:35+01:00
author: "Jens-Christian Fischer"
categories: ["code"]
tags: ["hugo", "tech" ]
language: en
slug:
type: post
---

# Hugo templating

I spent most of the time setting up this new blog deciding on which template to use. I settled
on [Casper-Two](https://themes.gohugo.io/hugo-casper-two/) but had to make changes literally minutes
after I started using it. I created a fork, [hugo-chaschper](https://github.com/jcfischer/hugo-chaschper) 
and made the following changes:

* Cleaned up (HTML formatting)
* Removing the 'caspertwo' options (Casper-Two contains two ways of displaying single page content. I 
  have started to remove the one I don't use)
* Added support for [IndieWeb](https://indieweb.org/) and [IndieAuth](https://indieauth.com/). I followed
  the post [IndieWebify Your Hugo Website](https://www.amitgawande.com/indiewebify-hugo-website/)
  
Things to do:

* Add my own pictures to the template
* Remove all superfluous partials
* Re-surrect the original CSS file so that I can change it
* CSS adaptions
* Atom feed
* [Webmentions](https://www.amitgawande.com/display-webmentions/)?
* [POSSE](https://indieweb.org/POSSE) - I will probably use [IFTTT](https://ifttt.com) for this
* 'Elsewhere' 
* Reading time
* Archives
* Better organisation of posts (internally)
* Expose Tags page
