---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-11-24 17:14:40+00:00
layout: post
link: http://invisible.ch/2004/11/24/doing-some-nasty-stuff-with-java-and-logging/
slug: doing-some-nasty-stuff-with-java-and-logging
tags: ["blog"]
title: doing some nasty stuff with java and logging
type: post
wordpress_id: 348
---

Remove all .debug stuff in existing java files:

[a handy SED reference](http://www.grymoire.com/Unix/Sed.html)

`
#!/usr/bin/sh

find . -type f -name '*.java' -print | while read i
do
# echo $i
echo "" >> $i
sed "s/^.*\.debug(.*)\s*;.*$/{;}/" $i > $i.tmp
sed "s/(.*\.isDebugEnabled()/(false/" $i.tmp > $i.tmp2
cp $i.tmp2 $i
done
`

Don't ask.
