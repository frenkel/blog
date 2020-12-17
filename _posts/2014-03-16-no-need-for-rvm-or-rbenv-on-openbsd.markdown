---
layout: post
title: "No need for RVM or rbenv on OpenBSD"
date: 2014-03-16 15:29:26 +0100
comments: true
categories: 
 - Programming
 - Webapps
 - OpenBSD
---
A lot of Ruby on Rails developers install Ruby by using [RVM](http://rvm.io) or [rbenv](https://github.com/sstephenson/rbenv). Most of the time this is because their operating system of choice comes without an up-to-date Ruby version. For example, Debian 7 ships Ruby 1.9.3 and Mac OS 10.8 shipped with 1.8.7. Tools like RVM or rbenv can be used to install a newer version in the users own home-directory. These tools use shims to "trick" `gem` and `bundle` into using the users own version instead of the system version. I've always found this to be a rather messy solution and luckily you don't need it on OpenBSD.
<!-- more -->
OpenBSD 5.4 has packages for Ruby 1.8.7, 1.9.3 and 2.0.0. The soon to be release OpenBSD 5.5 version also has a package for the 2.1.0 release! After installing one of these verions you will still need to install Bundler and some gems to develop your Rails application. This can be done by running `gem` with the `--user-install` option, which will install your gems in `~/.gem`. For example, to install Bundler run:
`gem install --user-install bundler`

By adding `~/.gem/ruby/<version>/bin` to your path you can now install the gems your project needs with the following command:
`bundle install --path ~/.gem`

This seems like a much cleaner way of working!

P.S. If your OS provides a recent version of Ruby, you can probably use the same steps to avoid RVM and rbenv.
