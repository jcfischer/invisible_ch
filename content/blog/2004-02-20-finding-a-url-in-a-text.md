---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2004-02-20 10:13:49+00:00
layout: post
link: https://invisible.ch/2004/02/20/finding-a-url-in-a-text/
slug: finding-a-url-in-a-text
tags: ["blog"]
title: Finding a URL in a text
type: post
wordpress_id: 252
---

**How do you find a URL in a normal text and turn it into a HTML link using regular expressions?** That was the challenge I faced recently. Oh - and of course not only well formed url's (with the https:// in front of them, but any kind of url.

Why invent something, when there's google to search? I found [Ben Forta's "How to match a URL"](https://www.forta.com/blog/index.cfm?mode=e&entry=992) but unfortunately it was way to forgiving in what it parsed, so I had to expand it a bit. Here are the results of a couple of hours of labor:
**UPDATE:** There was a nasty bug, that truncated all urls where the host started with the letters of one of the TLD's to the reminder ... _www.invisible.ch_ got truncated to _visible.ch_. The code below is corrected and simplified a bit (removed a couple of unneeded groups)
`
([\s]|^|<p>)
(https?://)?
(([\w]+?[-\w\.]+?\.)+
(a[cdefgilmnoqrstuwz]|b[abdefghijmnorstvwyz]|
c[acdfghiklmnoruvxyz]|d[ejkmnoz]|e[ceghrst]|
f[ijkmnor]|g[adefghilmnpqrstuwy]|h[kmnrtu]|
i[delmnoqrst]|j[emop]|k[eghimnprwyz]|
l[abcikrstuvy]|m[acdghklmnopqrstuvwxyz]|
n[acefgilopruz]|om|p[aefghklmnrstwy]|qa|
r[eouw]|s[abcdeghijklmnortvyz]|t[cdfghjkmnoprtvwz]|
u[ugkmsyz]|v[aceginu]|w[fs]|y[etu]|z[amw]|
com|edu|mil|gov|org|net|int|info|biz|name|pro
|museum|aero|coop){1})+
(:\d+)?
(/([\w/_\.]*(\?\S+)?)?)?
([\s]|</p>|<br />|$)
`
and then replace it with:
`$1>a href="$2$3$6$7"<$2$3$6$7>/a<$10`

Let's dissect this monster a bit, to see how it works:
<!-- more -->
`([\s]|^|<p>)`
Here we are looking for the beginning of the expression: Either a whitespace character (the [\s]) or the beginning of the line ( ^ ) or an opening paragraph tag ( <p;> ). If something matches this expression, it is stored in group number 1 ($1) for the replacmenet later.

`(https?://)?`
Next we are looking for the http scheme. The ? after the s means, either one or none of the preceding characters (which is the "s"). This part matches both "https://" and "https://". The question mark after the bracket group means either one or none of the following, making the scheme optional. 

`(([\w]+?[-\w\.]+?\.)+`
This part matches the host name and -- if found -- stores it in a numbered group. A host must start with a word character ( [\w]. We continue to match on word characters ( +? ). Because both "-" and "." are allowed in host names, we then expand the match to include these two characters ( [-\w\.]+? ) and match as long as we can. The whole group must at least match once.
So far we match things like "abc.def" or "a-b.de.f.g". The original regexp stopped here, but we are interested to have valid TLD (top level domains) so the next expresion matches the valid top level domains:

`(a[cdefgilmnoqrstuwz]|b[abdefghijmnorstvwyz]|
c[acdfghiklmnoruvxyz]|d[ejkmnoz]|e[ceghrst]|
f[ijkmnor]|g[adefghilmnpqrstuwy]|h[kmnrtu]|
i[delmnoqrst]|j[emop]|k[eghimnprwyz]|l[abcikrstuvy]|
m[acdghklmnopqrstuvwxyz]|n[acefgilopruz]|om|
p[aefghklmnrstwy]|qa|r[eouw]|s[abcdeghijklmnortvyz]|
t[cdfghjkmnoprtvwz]|u[ugkmsyz]|v[aceginu]|
w[fs]|y[etu]|z[amw]|
com|edu|mil|gov|org|net|int|info|biz|name|pro|
museum|aero|coop){1})+`
This looks worse than it it. Let's start at the end: (com|edu.... |coop) matches the known three- and more letter TLD's. The beginning matches the 240 different two-letter country TLD's. Instead of spelling out all 240 combinations, we use the slightly abbreviated form: `a[bcd]` which matches "ab", "ac" and "ad". Repeat ad nauseaum.

`(:\d+)?`
This part matches an (optional) port number (like :8080). The \d matches on a digit and the + says: repeat as long as there are digits.

`(/([\w/_\.]*(\?\S+)?)?)?` 
This piece matches any path's it the url ( foo.com/path ). The match has to start with a "/" followed by any combination of "word characters" (a-z, A-Z, 0-9), underscores or dot's, followed by either a question mark ( \?) or any non-whitespace (\S) character. That means, that paths with optional parameters ( ?foo=bar&head;=tail ) or funky characters ( 123,2334.html ) match.
Then there are a number of closing parentheses, that wrap up the different parts of the url and make them optional (with the ? ).

`([\s]|</p>|<br />|$)`
Finally the url is ended, when we match whitespace [\s] or a closing paragraph or a break or the end of the line ( $ )

Now that wasn't as bad, was it?

The replacment then is really simple:
`$1>a href="$2$3$6$7"<$2$3$6$7>/a<$10`
Remeber the groups I talked about earlier? The $1, $3 etc. represent those groups. So $1 is a variable that contains the content of the first match that was specfied in brackets in the searching regexp. (in this case, it contains the whitespace or start of line or paragraph tag). $2 contains the "http" scheme, $3 the host name, $6 the port number and $7 the path component. $10 finally contains whatever was after the url

So here you are: a search and replace expression that will fish out valid url's of a text and turn them into html links.
