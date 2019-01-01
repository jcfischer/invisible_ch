---
author: Jens-Christian Fischer
categories: ["musings"]
comments: true
date: 2005-05-03 11:54:15+00:00
layout: post
link: https://invisible.ch/2005/05/03/isyncing-with-the-nokia-9500/
slug: isyncing-with-the-nokia-9500
tags: ["blog"]
title: iSyncing with the Nokia 9500
type: post
wordpress_id: 406
---


After reading a bit about iSync & Tiger at [vowe](https://vowe.net/archives/005835.html), I decided to give the [solution outlined](https://www.macosxhints.com/article.php?story=20050422125043439) a try. However, I managed only to create a Kernel Exception on the phone, and to wipe out all my calendar entries.



Yes, I had a backup (through the excellent [mobical.net](https://www.mobical.net) service, which allows to sync the phone (and a lot of others) through GPRS.



Not giving up so easily (though it is tempting to drop the Nokia 9500 on Ebay and get a Trea 650 instead), I managed to export both contacts and calendar entries from mobical.net and import them into iCal / Address-Book on the Mac. One stumbling block was that the Addressbook only imported about 70 of 370 entries. Looking at the contacts.vcf file that mobical created, I noticed two entries with a PHOTO tag. Deleting those entries from the vcf-file got the import running.



Now I had all my data from the phone in my mac applications, but still no sync.



So I did, what every reasonable sane person in the same situation would do: 




  * Backup the phone through the Nokia PCSuite on my Dell Laptop


  * Perform a [factory reset](https://www.allaboutsymbian.com/forum/showthread.php?t=36358) on the Nokia 9500


  * Re-Do the steps as outlined in the [macosxhints article](https://www.macosxhints.com/article.php?story=20050422125043439)




Presto - syncing of calendar entries and addresses is now working. My Nokia 9500 got a spring cleaning and I can re-install those applications that are really necessary (Which it turns out, is quite a small number of applications)


Technorati Tags: [mac](https://technorati.com/tag/mac)
