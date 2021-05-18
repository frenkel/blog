---
layout: post
title: "Remote installation of OpenBSD from Linux"
description: "Install OpenBSD from within a Linux livecd without the need for official OpenBSD support at your hosting provider. Can be used when you have access to a virtual screen and keyboard."
date: 2014-04-13 19:09:05 +0200
comments: true
categories: 
- OpenBSD
---

Using a trick documented [here](http://www.narf.ssji.net/~shtrom/wiki/projets/whitedwarf), I switched this server from Linux to [OpenBSD](http://www.openbsd.org/), without a support installation method for OpenBSD from my ISP. In the original article, the author created a VM disk image and installed OpenBSD in it. The server was then rebooted into rescue mode (from a LiveCD) and the VM was uploaded and written to disk using dd. I modified the documented method a bit to speed up the process.
<!-- more -->
First I resized the Linux partition and added a new EXT2 partition at the end of the disk. EXT2 can be read and written from OpenBSD, this might be useful later. I created a small Linux installation with Qemu on that new partition. Next I installed Grub and configured it to use only the new partition. After a reboot in the new installation I booted Qemu with the old partition as its main disk, an OpenBSD installation ISO as its CD device and an ethernet card that uses the same driver (to avoid problems where hostname.if would be configured for the virtual card). Installation was just as simple when using a normal method. When the installation finished, I configured Grub to boot from the OpenBSD partition again and luckily had a succesfully booting system.

The biggest help for this process is the ability to remotely switch to a PXE booted kernel or rescue LiveCD. My ISP, [OVH](http://ovh.nl/), has this and I now always have the ability to boot the Linux partition in case of emergency by switching to PXE boot and setting the Linux partition as root device. 

For OVH it is also mandatory to set your IPv6 prefixlen to 56 instead of the default 64. Not doing so will result in problems when trying to reach their gateway.
