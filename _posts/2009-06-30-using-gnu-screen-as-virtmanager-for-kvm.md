---
title: Using GNU screen as virtmanager for KVM
author: frank
layout: post
permalink: /2009/06/30/using-gnu-screen-as-virtmanager-for-kvm/
date: 2009-06-30 19:10:16 +0100
categories:
  - Linux
tags:
  - console
  - debugging
  - kvm
  - Linux
  - nographic
  - screen
  - server
---
After my last post about KVM, somebody emailed me, asking how I use KVM&#8217;s serial console in combination with screen. It&#8217;s a rather simple, but really usefull solution if you think tools like virtmanager are too much for you and you don&#8217;t like to use VNC. So this post will try to explain it to you.  
For starters, you have to add the `-nographic` option to you KVM parameters. Next, make sure your virtual machine outputs it&#8217;s console to serial device 0. For example, start the Linux kernel with `console=ttyS0` and make sure there is a getty process running on that same device. Now, whenever you start KVM in a GNU screen (with that `-nographic` parameter) you will see the dmesg scroll by and will end up with a login prompt. You can just keep this KVM running while detaching the GNU screen session (ctrl+a d) and you can re-attach by starting `screen -x`.  
I use this on my server to start my two virtual machines. I made a screenrc like this:  
`# display a nice status bar on the bottom of the screen<br />
hardstatus alwayslastline "%-Lw%50>%n%f* %t%{-}%+Lw%< %=[%c]"<br />
vbell		off<br />
deflogin	off<br />
# use virtio for disks also!<br />
screen -t production kvm -m 2048m -nographic -drive file=production.raw,if=virtio,boot=on -net nic,model=virtio -net tap,ifname=tap0,script=no,downscript=no -smp 2<br />
screen -t development kvm -m 1024m -nographic -drive file=development.raw,if=virtio,boot=on -net nic,model=virtio -net tap,ifname=tap1,script=no,downscript=no`

Whenever the server boots it runs the following command in my rc.local:

`# start KVM<br />
cd /srv/<br />
su frank - -c 'screen -c screenrc -dm'`

So the server starts the GNU screen and the GNU screen start my virtual machines. If I can&#8217;t login via ssh in one of my virtual machines, I just connect to the host and attach to the screen to debug the problem.
