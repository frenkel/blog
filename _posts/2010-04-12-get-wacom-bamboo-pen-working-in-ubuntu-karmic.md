---
title: Get Wacom Bamboo Pen Working in Ubuntu Karmic
author: frank
layout: post
permalink: /2010/04/12/get-wacom-bamboo-pen-working-in-ubuntu-karmic/
date: 2010-04-12 18:20:35 +0100
categories:
  - Linux
tags:
  - 9.10
  - bamboo
  - compile
  - CTL-460
  - mouse
  - newer driver
  - pen
  - tablet
  - ubuntu
  - wacom
  - xorg
---
In my [last post][1] I described how to get the Wacom Bamboo Pen (CTL-460) to work in Ubuntu 10.04 Lucid. In this post I&#8217;ll explain how to get it working in Ubuntu 9.10 Karmic.<!--more-->

Getting the tablet to work in Karmic is a little bit more work. Most steps are the same, but the actual installation requires more than just copying the kernel module: you also need a new fdi file for hal and you need a new Xorg driver. For completeness, there are all the commands you need to execute.

First, install some compiling tools and header files:  
`sudo apt-get install build-essential libx11-dev libxi-dev x11proto-input-dev xserver-xorg-dev tk8.4-dev tcl8.4-dev libncurses5-dev`

Next, download the latest [linuxwacom][2] driver (0.8.6 at the moment of writing):  
`wget <a href="http://prdownloads.sourceforge.net/linuxwacom/linuxwacom-0.8.6.tar.bz2">http://prdownloads.sourceforge.net/linuxwacom/linuxwacom-0.8.6.tar.bz2</a>`

Now unpack, configure compile and install it:  
``tar -xf linuxwacom-0.8.6.tar.bz2<br />
cd linuxwacom-0.8.6<br />
./configure --enable-wacom<br />
make<br />
# I know 2.6.30 is the wrong number, but it's the highest available and it works just fine<br />
sudo cp src/2.6.30/wacom.ko /lib/modules/`uname -r`/kernel/drivers/input/tablet/<br />
sudo cp src/util/10-linuxwacom.fdi /usr/share/hal/fdi/policy/20thirdparty/10-linuxwacom.fdi<br />
sudo cp src/xdrv/wacom_drv.so /usr/lib/xorg/modules/input/wacom_drv.so``

Now restart hal, reload the wacom module and plug in your tablet:  
`sudo /etc/init.d/hal restart<br />
sudo rmmod wacom<br />
sudo modprobe wacom`

The tablet should work now. You can also add the module name to /etc/modules to automatically load it on boot. Same issues as in the previous post apply to Karmic, but for me this works good enough.

 [1]: https://frankgroeneveld.nl/2010/04/11/get-wacom-bamboo-fun-pen-working-in-ubuntu-lucid/
 [2]: http://linuxwacom.sf.net
