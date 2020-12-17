---
title: Pinnacle DVB-T stick on Ubuntu Jaunty
author: frank
layout: post
permalink: /2009/09/09/pinnacle-dvb-t-stick-on-ubuntu-jaunty/
date: 2009-09-09 13:29:17 +0100
categories:
  - Linux
tags:
  - dvb
  - dvb-t
  - dvb-t stick
  - dvbscan
  - jaunty
  - Linux
  - mplayer
  - pinnacle
  - ubuntu
---
Yesterday I decided to buy the Pinnacle DVB-T Stick (also known as Pinnacle TV Stick 72e) to watch some free-to-air channels. In the shop I searched on Google for Linux support, to make sure I didn&#8217;t have to return the product. The first few hits seemed positive (2 years ago), so I decided to take the plunge.

After arriving at home, I plugged the device in an empty USB port and saw this in my dmesg:

`<br />
[11906.080060] usb 1-6: new high speed USB device using ehci_hcd and address 5<br />
[11906.214249] usb 1-6: configuration #1 chosen from 1 choice<br />
[11906.245886] dib0700: loaded with support for 8 different device-types<br />
[11906.246212] dvb-usb: found a 'Pinnacle PCTV 72e' in cold state, will try to load a firmware<br />
[11906.246222] usb 1-6: firmware: requesting dvb-usb-dib0700-1.20.fw<br />
[11906.252816] dvb-usb: downloading firmware from file 'dvb-usb-dib0700-1.20.fw'<br />
[11906.471526] dib0700: firmware started successfully.<br />
[11906.972059] dvb-usb: found a 'Pinnacle PCTV 72e' in warm state.<br />
[11906.972135] dvb-usb: will pass the complete MPEG2 transport stream to the software demuxer.<br />
[11906.972367] DVB: registering new adapter (Pinnacle PCTV 72e)<br />
[11907.186126] DVB: registering adapter 0 frontend 0 (DiBcom 7000PC)...<br />
[11907.369975] DiB0070: successfully identified<br />
[11907.370122] input: IR-receiver inside an USB DVB receiver as /devices/pci0000:00/0000:00:12.2/usb1/1-6/input/input12<br />
[11907.396132] dvb-usb: schedule remote query interval to 50 msecs.<br />
[11907.396140] dvb-usb: Pinnacle PCTV 72e successfully initialized and connected.<br />
[11907.396744] usbcore: registered new interface driver dvb_usb_dib0700<br />
`

Great! All drivers and firmware load automatically in Ubuntu 9.04 Jaunty.

Next step: actually getting video on my screen. After Googling I found out I first had to scan for channels using dvbscan. However, it gave me the non-informal message &#8220;Unable to query frontend status&#8221;. Apparently there is also another scanning program called scan. I ran it like this:  
`scan /usr/share/dvb/dvb-t/nl-All > ~/.mplayer/channels.conf`  
Now I could start mplayer dvb:// and enjoy watching DVB-T digital television! Note you can switch channels with h (next) and k (previous). Last thing I need to figure out is how to use the remote for this (I can change the volume already).
