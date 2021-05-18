---
layout: post
title: "Pro Pupppet Second Edition Review"
date: 2014-03-30 20:32:40 +0200
comments: true
categories:
- Books
- Review
- Linux
---

A few weeks back I purchased Pro Puppet for my Kindle. I had been using Puppet before, but reading this book gave me more insight in how to use Puppet and made me start using Puppet again.
<!-- more -->
The first chapter gives an explanation on how to get Puppet going on various systems, which I skipped for a great part: I'm only interested in the Debian installation, but had already followed the guide on the Puppetlabs website.

In chapter two it did get interesting. Some important concepts such as variable scope, modules and inheritence are demonstrated by building various modules that install and configure services. I found these practical examples a great way to learn more about the syntax and preferred techniques (try to avoid inheritance!). Based on these chapters I wrote some modules for [Ivaldi](http://ivaldi.nl/), that allow us to easly create a system user, database, database user, grant permissions and configure an Apache virtual host on our servers.

The next chapter provides ways to apply the Puppet configuration to your systems. Most people will use the Puppet master & agent setup: the master is a server that provides all agents with their needed configuration files. However, it's also possible to skip the master and use the agent stand-alone, combined with a way to distribute your configuration (for example using a version-control system). The last part of this chapter introduces a Git hook that can be used to push a Git repository containing your configuration to all your servers. The Git hook will start the Puppet agent and apply the configuration.

For some bigger setups, the default master/agent setup won't scale well enought. Therefor, a complete chapter is provided that explains how to scale and load balance Puppet. I didn't need this chapter, but it was an interesting read, because I'm now more prepared what to expect when my amount of servers grows too big.

I didn't find chapter five that interesting: it's an explanation about external node classification. This can be used to avoid adding every seperate server to your configuration. As you can guess this is only interesting if you have hundreds of servers.

The next few chapters touched all kinds of concepts: 

- Virtual Resources, which can be used to fake a configured resource.
- Exported Resources, a great way to configure a service based on another configured node. The example in the book configures a Nagios server that automatically monitors all other nodes configured with Puppet. This was interesting!
- Various front-ends and consoles to Puppet: Foreman, Puppet Enterprise and Puppetboard.
- Reporting and monitoring of Puppet.
- Testing Puppet modules, an interesting read.
- Managing module dependencies using Librarian or R10K.
- Hiera and data seperation.

All in all I was glad I bought this book. Some parts were not that interesting for a small scale setup, but I can imagine most people only start using Puppet when their manual configuration becomes too much of a burden. A recommended read for anybody who want to improve his server setup!
