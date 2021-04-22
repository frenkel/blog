---
layout: post
title: "Fighting Spam with OpenBSD's spamd(8)"
date: 2014-04-27 17:11:53 +0200
comments: true
categories: 
- OpenBSD
---
A few days ago I discoved OpenBSD's [spamd(8)](http://www.openbsd.org/cgi-bin/man.cgi?query=spamd&section=8). Apparently I've always confused it with [SpamAssassin's daemon](https://spamassassin.apache.org/full/3.0.x/dist/doc/spamd.html), which is also called spamd. OpenBSD's spamd is a lot more light weight than SpamAsssasin, but it's tactics to fight spam are fairly effective. I'll explain how it works below.
<!-- more -->

Botnets that sent spam are focused on delivering as much as possible in a short time. If the mail server they connect to asks them to try again later, most of them will just give up and not retry the delivery. This is exactly what spamd uses to prevent spam. It defers the spam, resulting in a lot less deliveries.

Spamd uses three lists of ip addresses: a whitelist, a greylist and a blacklist. When an ip address of the whitelist connects to the server, it is directly forwarded to the real SMTP daemon. This is done using the firewall, meaning spamd will maintain the whitelist for the firewall.

The greylisted addresses are first directed to spamd, which will give it a "try again in *x* minutes" message. When a mail server reconnects after the specified time, it will be added to the whitelist for a configurable amount of days. Everytime the server reconnect in this interval, the experiation time is moved forward. This keeps fairly active mailservers in the whitelist for ever.

The blacklisted addresses are slowly told that there was a permanent error when trying to deliver their message. The purpose of this slow down is to use as much resources of the sender as possible in order to annoy them.

Setting up spamd on your OpenBSD system is quite easy, just follow [the instructions in the manpage](http://www.openbsd.org/cgi-bin/man.cgi?query=spamd&section=8).
