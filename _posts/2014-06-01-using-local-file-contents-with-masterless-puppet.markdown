---
layout: post
title: "Using Local File Contents With Masterless Puppet"
date: 2014-06-01 21:01:11 +0200
comments: true
categories: 
---

For a masterless Puppet setup I use to configure my personal computers, I was in need of a way to cleanup all my inline file declarations. <!-- more --> I had a lot of things like this:

    file { '/home/frank/.profile':
      ensure => present,
      content => "PATH=$HOME/bin:/bin:/sbin:/usr/bin:/usr/sbin:/usr/X11R6/bin:/usr/local/bin:/usr/local/sbin:/usr/games:.
      CVSROOT=anoncvs@openbsd.cs.fau.de:/cvs
      HISTFILE=~/.sh_history
      PS1='\u@\h:\w\$ '
      export PATH HOME TERM CVSROOT HISTFILE PS1
      ",
    }

This gets messy real fast, especially because of the needed newlines and crappy indentation. After reading the Puppet Type Reference I didn't think I could use the source attribute of "file". However, when using modules in combination with a masterless setup, it does work the same as a setup with Puppet master, as long as you pass `--modulepath` to the `puppet apply` command. The previous example is now written as:

    file { '/home/frank/.profile':
      ensure => present,
      source => 'puppet:///modules/openbsd/dot.profile',
    }

The actual file contents can be stored in `modules/openbsd/files/dot.profile`, just like when using a Puppet master. That's a lot cleaner!
