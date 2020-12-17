---
title: Using Nagios to monitor multiple VirtualHosts
author: frank
layout: post
permalink: /2012/03/08/using-nagios-to-monitor-multiple-virtualhosts/
date: 2012-03-08 19:53:39 +0100
categories:
  - Linux
  - Webapps
tags:
  - monitoring
  - nagios
  - php
  - www
---
On first sight, it doesn&#8217;t look like Nagios or Icinga can be used to monitor websites hosted on the same server. All concepts in Nagios and Icinga revolve around services and hosts. The whole &#8220;sub-part of a service&#8221;, like a VirtualHosts in the HTTP service, doesn&#8217;t seem to fit. It is perfectly possible though.

Let&#8217;s start by adding three simple commands that use check_http with various arguments to make sure the VirtualHost is returning a page correctly. Paste the following in your command config, for example in /etc/icinga/object/commands.cfg

<pre>
define command {
        command_name check_http_vhost
        command_line /usr/lib/nagios/plugins/check_http -I '$HOSTADDRESS$' -k 'Host: $ARG1$'
}

define command {
        command_name check_https_vhost
        command_line /usr/lib/nagios/plugins/check_http -S -I '$ARG1$' -k 'Host: $ARG1$'
}

define command {
        command_name check_http_vhost_url
        command_line /usr/lib/nagios/plugins/check_http -I '$HOSTADDRESS$' -k 'Host: $ARG1$' -u '$ARG2$'
}
</pre>

This will add three commands to your config, allowing you to check a normal VirtualHost, an https VirtualHost and a normal VirtualHost on a certain url (this can be handy if your front page redirects to a logiin page for example). 
You can now add a service definition to a server for every VirtualHost you want to monitor. For example:

<pre>define service {
        host_name               yourservername
        service_description     domainone.com
        check_command           check_http_vhost!domainone.com
        use                     generic-service
}

define service {
        host_name               yourservername
        service_description     domaintwo.com
        check_command           check_https_vhost!domaintwo.com
        use                     generic-service
}
define service {
        host_name               yourservername
        service_description     domainthree.com
        check_command           check_http_vhost_url!domainthree.com!/sessions/new
        use                     generic-service
}</pre>

Good luck!
