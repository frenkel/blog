---
title: My first Cherokee patch
author: frank
layout: post
permalink: /2009/05/24/my-first-cherokee-patch/
date: 2009-05-24 09:16:30 +0100
categories:
  - Linux
  - Programming
tags:
  - cherokee
  - mysql
  - patch
  - server
  - sha1
  - subversion
  - webdav
---
I&#8217;ve been playing with [Cherokee][1] (the light-weight web server) for a while now. I really like the way their configuration file can be managed with cherokee-admin. This is basically a secured web page that provides a convenient interface to all of Cherokees settings.  
Although Cherokee is looks so great, I can&#8217;t switch the [Ivaldi][2] web server to it, because of a few problems:

*   No support for authentication against SHA1 hashed passwords from a MySQL database
*   No support for webdav/svn, we currently use Apaches mod_subversion with authentication against a MySQL database.

The first point didn&#8217;t seem so hard to fix, so I [submitted a patch][3] to the Cherokee project. The maintainer got in contact with me and let me sign a contributors agreement. I think this means that the code can be committed to their subversion repositories now.  
This still leaves one problem before I can switch: webdav/svn. I don&#8217;t think I have enough knowledge to fix that. I might try to switch all our current sites to Cherokee though and keep a light-weight, trimmed down, Apache for webdav/svn.

 [1]: http://cherokee-project.com
 [2]: http://ivaldi.nl
 [3]: http://code.google.com/p/cherokee/issues/detail?id=477
