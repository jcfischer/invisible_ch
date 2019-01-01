---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-06-02 10:00:29+00:00
layout: post
link: http://invisible.ch/2005/06/02/emacs-on-osx-for-rails-development/
slug: emacs-on-osx-for-rails-development
tags: ["blog"]
title: EMacs on OS/X for Rails development
type: post
wordpress_id: 417
---


Being a step-by-step guide as an aide for the failing memory. Inspired by the [screenshots of Dee Zsombor](http://deezsombor.blogspot.com/2005/05/ide-options.html)




  * Get a [Tiger compatible Emacs](http://home.att.ne.jp/alpha/z123/emacs-mac-e.html)


  * (unfortunately [Aquamacs](http://sourceforge.net/project/showfiles.php?group_id=138078)  does strange (i.e non-emacs) things with it's windows, so ECB falls on it's face)


  * Install RubyMode.el (from the Ruby distribution)


  * [Download ECB](http://ecb.sourceforge.net/)


  * [Download  supporting libraries](http://sourceforge.net/project/showfiles.php?group_id=17886&release_id=254753) (eieio, speedbar, semantic) and install them (usually make, make install and an entry in .emacs)


  * [Download MMM](http://mmm-mode.sourceforge.net/) (Multiple-Major-Modes) so you have support for both HTML and ERB in those .rhtml files


  * get [ruby-electric.el](http://shylock.uw.hu/Emacs/ruby-electric.el) and install it


  * [find the SVN mode](http://svn.haxx.se/users/archive-2004-09/0327.shtml) for Emacs and install it


  * [Scott has some tips](http://scott.elitists.net/users/scott/posts/rails-on-emacs) on MMM and ERB templates


  * [ido.el](http://www.cua.dk/ido.html) is a nice extension for switching buffers and finding files




All my extensions are in ~/lisp and that file (as well as ~/.emacs) are under version control in Subversion. That way, I can check out my workspace on any machine and have a configured way of doing things.



see my [.emacs](/.emacs)  file for a possible way of doing this



All of this should work on a Windows box too





Technorati Tags: [emacs](http://technorati.com/tag/emacs), [ruby on rails](http://technorati.com/tag/ruby on rails)
