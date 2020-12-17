---
title: Dropbox on Your Own Server
author: frank
layout: post
permalink: /2010/08/03/dropbox-on-your-own-server/
date: 2010-08-03 17:21:57 +0100
categories:
  - Linux
  - Programming
tags:
  - dropbox
  - git
  - Linux
  - open source
  - release
  - sparkleshare
---
I&#8217;ve always liked [Dropbox][1], except for one thing: I don&#8217;t trust them with my data. Also, it seems wrong to pay $ 10,00 for 50 GB of storage when you have your own server with much more storage and available on a fast network.<span style="color: #808080;"><br /> </span>

Well, finally there is a solution. It&#8217;s called [SparkleShare][2] and it&#8217;s completely open source and uses [Git][3] as a backend. Today [they released ][4]a very early alpha version and I tried it out immediately. After having some trouble with the interface (you need to insert <username>/<reponame> in the folder input box if you use Github), everything worked great. However, I don&#8217;t advice anybody to use it in production. It&#8217;s still in development and can contain serious bugs. I can&#8217;t wait till it gets more mature and ready for production usage!

 [1]: https://www.dropbox.com/referrals/NTU3NDI2Njk5
 [2]: http://www.sparkleshare.org/
 [3]: http://git-scm.com/
 [4]: http://www.bomahy.nl/hylke/blog/sparkleshare-02-alpha-1-for-linux/
