---
title: Automatic Invariant Detection in Dynamic Web Applications
author: frank
layout: post
permalink: /2010/09/08/automatic-invariant-detection-in-dynamic-web-applications/
date: 2010-09-08 17:49:49 +0100
categories:
  - Programming
  - Webapps
tags:
  - crawljax
  - dynamic
  - invariants
  - invarscope
  - paper
  - plugin
  - thesis
  - web applications
---
For the last year, I have been working on my master project and two weeks ago I finally graduated. I did my master project at [Tam Tam][1], an internet agency that provides full service internet services. It was nice to work there and if I did not have the opportunity to expand [my own company][2] I would have applied for a job at Tam Tam.

The project was about automatically finding invariants in web applications. The first focus was finding invariants in the JavaScript parts, but later on we extended the scope a bit and also included invariants over the DOM. While most of the techniques I developed can be used in a very generic way, my implementation depends on [Crawljax][3]. I developed plugins to Crawljax, under the name of [InvarScope][4], that can automatically find these invariants and use them for regression testing.

We submitted a paper based on my work to [ICSE&#8217;11][5], so before that was finished I was not allowed to blog or publish any of my work. Well, we made the deadline, so I can now release all of the code, [my thesis][6] and the [paper][7] itself.

The code I wrote is available in a [subdirectory of the Crawljax plugins Google code project][8]. We&#8217;re currently in the process of fixing all Maven dependencies, cleaning up some code and making it all work with the current Crawljax trunk version, so expect a binary release in a few days.

Don&#8217;t hesitate to contact me if you have any questions!

 [1]: http://www.tamtam.nl/
 [2]: http://ivaldi.nl/
 [3]: http://crawljax.com/
 [4]: http://crawljax.com/plugins/invarscope-plugins/
 [5]: http://2011.icse-conferences.org/
 [6]: https://frankgroeneveld.nl/wp-content/uploads/2010/09/thesis-frank-groeneveld1.pdf
 [7]: http://swerl.tudelft.nl/twiki/pub/Main/TechnicalReports/TUD-SERG-2010-037.pdf
 [8]: http://code.google.com/p/crawljax-plugins/source/browse/#svn/trunk/invarscope
