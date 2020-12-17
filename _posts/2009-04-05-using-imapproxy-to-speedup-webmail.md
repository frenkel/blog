---
title: Using imapproxy to speedup webmail
author: frank
layout: post
permalink: /2009/04/05/using-imapproxy-to-speedup-webmail/
date: 2009-04-05 15:11:54 +0100
categories:
  - Linux
tags:
  - imap
  - proxy
  - server
  - webmail
---
Yesterday, I discovered a great way to improve the speed of your webmail client. Two friends of mine were talking about something called imapproxy.  
Apparently this is a simply brilliant tool. It was invented because the web is stateless, but imap is not. Your webmail client (for example Roundcube) will reconnect to the imap server everytime you click a link or refresh. This introduces a great deal of lag. The solution to this problem is imapproxy. Your webmail client connects to the proxy and imapproxy opens a connection to the imap server. When the webmail client disconnects, the proxy keeps the connection open for another 5 minutes, so when you refresh or change directory, this can be done very fast!  
I installed imapproxy on the webserver of my company. At first I couldn&#8217;t get it to work, because I wanted it to connect to imap over ssl, but after enabling &#8220;plain text&#8221; imap for localhost, I let imapproxy connect to it and everything worked. The roundcube installation now reacts almost instantly!  
So remember, don&#8217;t try to let imapproxy use ssl, because the only error you will notice is that imapproxy is not listening on any port. The developers just forgot to add error reporting I guess.
