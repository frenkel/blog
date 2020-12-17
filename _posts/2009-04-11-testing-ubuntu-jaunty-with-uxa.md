---
title: Testing Ubuntu Jaunty with UXA
author: frank
layout: post
permalink: /2009/04/11/testing-ubuntu-jaunty-with-uxa/
date: 2009-04-11 17:02:48 +0100
categories:
  - Linux
tags:
  - compiz
  - intel
  - jaunty
  - Linux
  - ubuntu
  - uxa
---
I&#8217;ve been testing Ubuntu Jaunty for a few weeks now and after using it for a day or two, my memory filled up. Recently I found out that this was caused by Compiz. Apparently if you use UXA with the new Intel drivers, Compiz will start to leak memory. After only 8 hours of usage, Compiz was using more than 1.5GB of memory! The solution? Disable Compiz, because UXA is a big performance improvement for me.

**Update:** Apparently this bug is fixed ([#328232][1]).

 [1]: https://bugs.launchpad.net/ubuntu/+source/compiz/+bug/328232
