---
title: 'Howto: Live migrate to software RAID 1'
author: frank
layout: post
permalink: /2009/09/19/howto-live-migrate-to-software-raid-1/
date: 2009-09-19 15:22:54 +0100
categories:
  - Linux
tags:
  - degraded
  - jaunty
  - Linux
  - mdadm
  - raid
  - software raid
  - striping
  - ubuntu
---
Feel insecure about your data? Don&#8217;t trust your harddrive anymore? Use this howto to migrate your running Ubuntu Linux system to software RAID&nbsp;1.

Before starting off, I assume you have your running system on /dev/sda and your new harddrive is called /dev/sdb.

Boot up your system and install the mdadm package. We now have to create partitions on sdb that are the same as sda. Because I have identical disks, I just copy the partition table from sda to sdb like so:  
`sfdisk -d /dev/sda | sfdisk /dev/sdb`  
After that, I use partprobe to let the Linux kernel know I have changed the partition table.

Next step is to create a degraded RAID array on sdb which we can copy the files to and than add sda to the array. For every partition you have to run:  
`mdadm --create /dev/md0 --level 1 --raid-devices=2 missing /dev/sdb1<br />
`  
Where you replace sdb1 with the partition you want. Now create filesystems on these new raid devices:  
`mkfs.ext3 /dev/md0`  
Again, run this for all your mds.  
After copying all the files to your new array, we have to modify a few files.

*   /boot/grub/menu.lst
*   /etc/fstab
*   /etc/initramfs-tools/conf/resume

All these files contain references to UUIDs that are no longer correct. I simply replaced them with /dev/md0 for example. You can try to use UUIDs, but I believe that the (striped) partitions have the same UUIDs as the raid devices (the mds). If you&#8217;ve changed everything, run:  
`mdadm --detail --scan >> /etc/mdadm/mdadm.conf`  
And don&#8217;t forget to update your initrd:  
`initramfs -u`

That&#8217;s all! You can now enjoy the safety of RAID 1 without to much hassle. To check the status of your array, look in /proc/mdstat. Also make sure you setup a mail server or ssmtp, because the mdadm tools will try to send you an email if one of your RAID devices is degraded/corrupt.
