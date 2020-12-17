---
title: Pinnacle DVB-T stick remote
author: frank
layout: post
permalink: /2009/09/12/pinnacle-dvb-t-stick-remote/
date: 2009-09-12 17:48:15 +0100
categories:
  - Linux
tags:
  - '&gt;255'
  - dvb-t
  - events
  - jaunty
  - keyboard
  - keycode
  - Linux
  - pinnacle
  - remote
  - ubuntu
  - x11
  - x12
---
Another post about that Pinnacle DVB-T stick? No, this one is about the remote! I wrote that the remote wasn&#8217;t completely working yet. Apparently, there is a driver for this remote or the stick that converts the buttons from the remote to &#8220;keyboard events&#8221;. Meaning I can type the number 0-9 with my remote for example. However, the &#8220;change channel&#8221; buttons appear to send a keycode that is above 255 and the X11 protocol only reserves one byte for keycodes. This means those keycodes can&#8217;t be send to the X11 server and will disappear. There&#8217;s a bug about this in the X.org bugzillay: <http://bugs.freedesktop.org/show_bug.cgi?id=x11-keycode-limit> and their solution: Change the X11 protocol (meaning: start development on the X12 protocol) or remap those keyevents somewhere between the kernel and X.org. I think the last solution is probably the simplest. I only have to figure out how to remap those keys with hal.
