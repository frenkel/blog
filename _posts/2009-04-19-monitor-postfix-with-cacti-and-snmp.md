---
title: Monitor Postfix with Cacti and SNMP
author: frank
layout: post
permalink: /2009/04/19/monitor-postfix-with-cacti-and-snmp/
date: 2009-04-19 20:50:42 +0100
categories:
  - Linux
tags:
  - cacti
  - monitoring
  - postfix
  - server
  - snmp
  - spam
---
Today I configured Cacti and SNMP after I saw the graphs of a friend. He had graphs for Postfix, which showed statics like sent/received/rejected.  
After a little search on the internet, I found [a post][1] on the Cacti forum. At first I couldn&#8217;t get it to work, but after running the script manually (instead of via SNMPd) I found out /var/log/mail.log was not readable by the SNMP user.  
Cacti has been polling snmp for the past few hours now and apparently I receive around 25 spam emails that get rejected every 5 minutes. That&#8217;s 6000 mails per day, more than 2.000.000 every year. I&#8217;m glad I configured postfix to reject those mails (have a look at the reject\_rbl\_client config directive of postfix).

 [1]: http://forums.cacti.net/post-51584.html#51584
