---
title: Get Wacom Bamboo Pen Working in Ubuntu Lucid
author: frank
layout: post
permalink: /2010/04/11/get-wacom-bamboo-fun-pen-working-in-ubuntu-lucid/
date: 2010-04-11 15:10:28 +0100
categories:
  - Linux
tags:
  - 10.04 LTS
  - bamboo
  - compile
  - CTL-460
  - Linux
  - lucid
  - mouse
  - newer driver
  - pen
  - tablet
  - ubuntu
  - wacom
  - xorg
---
The new [Wacom Bamboo Pen (CTL-460)][1] doesn&#8217;t work in [Ubuntu][2] Lucid out-of-the-box. You need a newer kernel module than the one that comes with Lucid by default. It&#8217;s pretty easy to get it working though, you just need to know how.<!--more-->

### Update

It seems that since I published this post four months ago, it helped a lot of people. At that time I couldn&#8217;t find a [DKMS][3] script that would automatically compile and install the newer module after every kernel upgrade. Also, I didn&#8217;t have the time to do it myself. Well, things have changed. After Brett Alton posted his [update to my post][4]. Martin Owens replied to his post with a link to a PPA that contains the newer module with a DKMS script. So please, use this PPA and save yourself a lot of trouble! The instructions are really simple, just run this in a terminal:

`sudo add-apt-repository ppa:doctormo/wacom-plus<br />
sudo apt-get update<br />
sudo apt-get install wacom-dkms`

**Don&#8217;t forget** to [register your tablet][5] at the Wacom website, because you can specify Linux as your operating system. We might get even better support if a lot of people do this.

### Old post:

First, install some compiling tools and header files:  
`sudo apt-get install build-essential libx11-dev libxi-dev x11proto-input-dev xserver-xorg-dev tk8.4-dev tcl8.4-dev libncurses5-dev`

Next, download the latest [linuxwacom][6] driver (0.8.6 at the moment of writing):  
`wget <a href="http://prdownloads.sourceforge.net/linuxwacom/linuxwacom-0.8.6.tar.bz2">http://prdownloads.sourceforge.net/linuxwacom/linuxwacom-0.8.6.tar.bz2</a>`

Now unpack, configure compile and install it:  
``tar -xf linuxwacom-0.8.6.tar.bz2<br />
cd linuxwacom-0.8.6<br />
./configure --enable-wacom<br />
cd src/2.6.30/ # I know this is the wrong version, but it's the highest available and it works<br />
make<br />
sudo cp wacom.ko /lib/modules/`uname -r`/kernel/drivers/input/tablet/<br />
sudo rmmod wacom<br />
sudo modprobe wacom``

The tablet should work now. You can also add the module name to /etc/modules to automatically load it on boot. There still one issue left for me. In Mac OS X I can use the whole tablet, i.e. the right corner is the right screen corner. In Lucid however the grey lines indicate the screen borders, so the right corner of the gray lines is the right screen corner. This means part of the tablet is not used and this can be quite annoying if you&#8217;re used to the previous behavior.

**Don&#8217;t forget** to [register your tablet][5] at the Wacom website, because you can specify Linux as your operating system. We might get even better support if a lot of people do this.

 [1]: http://www.wacom.com/bamboo/bamboo_pen.php
 [2]: http://ubuntu.com
 [3]: http://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support
 [4]: http://blog.brettalton.com/2010/08/28/how-to-install-the-wacom-bamboo-driver-in-ubuntu-10-04-lucid-lynx/
 [5]: http://www.wacom.com/register/index.php
 [6]: http://linuxwacom.sf.net
