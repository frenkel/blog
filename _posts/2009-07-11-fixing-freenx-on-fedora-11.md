---
title: Fixing FreeNX on Fedora 11
author: frank
layout: post
permalink: /2009/07/11/fixing-freenx-on-fedora-11/
date: 2009-07-11 22:41:08 +0100
categories:
  - Linux
tags:
  - fedora
  - freenx
  - Linux
  - nx
  - xorg
---
Today I had some problems getting FreeNX to work on Fedora 11. FreeNX is a VNC-like system that has much better performance than VNC itself. It is therefore very usefull if you would like to access your computer via your Cable or ADSL connection.

After installing FreeNX in Fedora, whenever I connected, I got some strange error messages. The error message also told me to run some command via ssh to find out more. Apparently, FreeNX wanted to start on display port :0, which was already in use by X. To fix this, I copied /etc/nxserver/node.conf.sample to /etc/nxserver/node.conf and uncomment the line that says: `DISPLAY_BASE=1000` and change it to `DISPLAY_BASE=1001`. This will start the NX server on port 1001 (display port :1).  
However, this fix would still not allow me to connect. After searching around on the internet, I found out the package was missing a dependency on xorg-x11-fonts-misc. Installing it allowed me to open a session and enjoy the responsiveness of FreeNX!

In short: Make sure your DISPLAY_BASE port is not set to 1000 if you also have another X server running and don&#8217;t forget to install xorg-x11-fonts-misc.
