---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2010-04-12 15:02:01+00:00
layout: post
link: http://blog.invisible.ch/2010/04/12/gpg-mail-under-snow-leopard/
slug: gpg-mail-under-snow-leopard
tags: ["blog"]
title: GPG Mail under Snow Leopard
type: post
wordpress_id: 803
---

For an upcoming project I needed to set up secure communications using GPG. It's been a few years since I used this, and I have never used GPG on the Mac before... Turn out, that it's not trivial to get it running... Here's a bunch of links that helped me get things working:


* [http://macgpg.sourceforge.net/index.html](http://macgpg.sourceforge.net/index.html) - the main MacPGP website
* it includes [this readme to compile under SnowLeopard](http://macgpg.sourceforge.net/docs/howto-build-gpg-osx.txt.asc). The important part is this line: `./configure CC="gcc -arch i386"`
* You will at least need the GPGKeychain and the GPG Preference Pane from the page above - it's precompile and "should just work" 
* The [GPGMail plugin for SnowLeopard](http://github.com/lukele/GPGMail-SL) - you can download a ZIP file with the .mailbundle

Then generate your keys (follow the instructions found at [Zeitform](http://fiatlux.zeitform.info/en/instructions/pgp_macosx.html))

To install the mailbundle, create a folder `~/Library/Mail/Bundles` and copy the GPGMail.mailbundle file you downloaded from Github into it. Drop to a terminal and execute the following two command which will enable Bundles in Mail.app.

`
defaults write com.apple.mail EnableBundles -bool yes`  

`defaults write com.apple.mail BundleCompatibility -int 3
`  

(via [blogator](http://www.blogator.de/macos/gpgmail-fur-leopard/)) 

Now you can start importing public keys from others into you GPG Keychain and sign / encrypt email from Mail.app

Here is my GPG public key [0x3B5F40BE](http://invisible.ch/assets/64/0x3B5F40BE.asc)
