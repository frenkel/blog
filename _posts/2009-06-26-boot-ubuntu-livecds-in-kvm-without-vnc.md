---
title: Boot Ubuntu livecds in KVM without VNC
author: frank
layout: post
permalink: /2009/06/26/boot-ubuntu-livecds-in-kvm-without-vnc/
date: 2009-06-26 09:07:07 +0100
categories:
  - Linux
tags:
  - kvm
  - no vnc
  - nographic
  - screen
  - serial console
  - server
  - ubuntu
---
This post is just for the sake of documenting this.

A while ago I came across a blog post written by an Ubuntu developer (I believe) which gave a nice tip on how to boot a livecd in KVM without VNC. Yesterday I needed this feature again, but was unable to find it.

I needed to boot a hardy-jeos livecd on my server, but didn&#8217;t want to go through the hassle of punching a hole in my firewall and installing a vnc client on my desktop computer. Luckily this is not needed, because you can get kvm to output it&#8217;s serial console to your console (in combination with GNU Screen this is very usefull) and the livecd support serial console also. To do all this you just need to append this to your kvm startup command:  
`-nographic -kernel /mnt/install/vmlinuz -append console=ttyS0,9600 -initrd /mnt/install/initrd.gz -cdrom /home/frank/hardy-jeos-i386.iso`  
Of course, the relevant files should be changed according to your system. Note that the kernel and initrd files are on the cd, so you should mount the cd on the host sytem also.

Any questions? Just leave them in the comments!
