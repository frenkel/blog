---
title: Speeding up your website
author: frank
layout: post
permalink: /2009/06/28/speeding-up-your-website/
date: 2009-06-28 15:17:50 +0100
categories:
  - Programming
tags:
  - google
  - html
  - optimizing
  - php
  - speeding up
  - xhtml
---
A few days ago I stumbled upon the new Google [&#8220;Let&#8217;s make the web faster&#8221;-page][1]. I found some useful tips on there. Some of them are [public knowledge][2], for example the fact that using echo in php is faster than print, single quotes are faster than double quotes and echo supports endless arguments, which is faster than string concatenating (so you write `echo 'this', $is, 'faster than', $concatenating, 'the string'` instead of `echo 'this' . $is . 'slower'`).  
However, there&#8217;s a nice article about [ommitting html tags][3], which had some tips I did not know. For example, if you&#8217;re using HTML, instead of XHTML, you&#8217;re allowed to ommit more tags than most people know. For example, you don&#8217;t need to close a paragraph, you can just start a new one. For the complete list, have a look at the articles section of the site.

 [1]: http://code.google.com/speed/
 [2]: http://code.google.com/speed/articles/optimizing-php.html
 [3]: http://code.google.com/speed/articles/optimizing-html.html
