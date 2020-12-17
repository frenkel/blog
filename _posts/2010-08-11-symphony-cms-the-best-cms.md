---
title: Symphony CMS; the Best CMS?
author: frank
layout: post
permalink: /2010/08/11/symphony-cms-the-best-cms/
date: 2010-08-11 19:17:34 +0100
categories:
  - Programming
  - Webapps
tags:
  - best
  - cms
  - expression engine
  - open source
  - symphony
  - wordpress
---
I&#8217;ve been looking for a good Content Management System (CMS) the last couple of days after a colleague and I had some discussion about what CMS to use for our clients. Sometimes we have clients with specific needs, which are difficult to fulfill using [WordPress][1]. The solution we used to choose was either build some plugins or use our custom developed CMS. However, none of these are a great solution. WordPress can be complicated for novice computer users, has a messy code-base and our own CMS is not really user-friendly either.

My colleague decided to try out [ExpressionEngine][2]. He bought the freelancer edition and he&#8217;s been trying things out. Up until now, it all seems to work quite well, although the back-end can still be too complicated for our clients. Also, I hate the fact that you should pay 300 dollars to use ExpressionEngine for a commercial company. Thats an added fee some customers would rather spend on different things.

So, I started to search for open-source CMSes myself and made a list of requirements.

*   It should not be page based, it should allow you to model your own content. If you use a CMS that supports types/entities/resources/sections/whatever you can create your own page type, but you can also create more advanced things like portfolio items, projects or products (yes, even a simple web shop is possible then).
*   The back-end should be as simple as possible.
*   It should be written in PHP, object-oriented if possible, and use MySQL for storage.
*   There should be a good, flexible templating engine for the views.
*   It should have a good plugin API.

Well, using this list it was a lot easier to search for the most fitting CMS, as quite a lot CMSes are only page or post based. The list of possible candidates shrunk by more than 75%. Eventually I found a CMS I had never heard of, but which seemed to have all the things we were looking for: Symphony CMS.

I&#8217;ve been trying it out in the last few days and I still haven&#8217;t found any deal-breakers. [Symphony CMS][3] has a great website, friendly community (because it&#8217;s still small I think), great features, simple back-end, small code-base and it can be easily extended by writing extensions.

Some things might give problems for specific clients though: multi file upload is non-existant (there&#8217;s one extension that doesn&#8217;t do what it should) and the WYSIWYG editor extensions, with support for placing images etc., don&#8217;t seem to be integrated well enough with Symphony CMS yet. Well, maybe I&#8217;ll just fix those two myself and contribute them upstream. That is, if I have some spare time ;)

 [1]: http://wordpress.org/
 [2]: http://expressionengine.com/
 [3]: http://symphony-cms.com/
