---
layout: post
title: "Reduce number of Jira notification mails"
date: 2020-12-30 18:49:59 +0100
comments: true
categories: Workflow
---

The past few months I've been fine-tuning a mail filter to reduce the amount of Jira notification
mails I receive in my inbox. Last year Atlassian already improved the experience quite a bit, but
I still get a lot of notifications I don't care about.

## Notification I do care about
I only care about notifications for me being mentioned or assigned. Furthermore I want to read
comments on issues I watch and new issues that are created with me as the assignee.

## Solution

The solution I've made is quite simple. It relies on a filter rule that is applied to incoming
emails:

1. Filter mails from the Jira email address.
2. Make sure they do not contain one of these words:
- mentioned
- assigned
- comment
- created
3. Let them be moved to the trash.

I'm quite happy with how well this works. It has removed a lot of noise from my inbox.
