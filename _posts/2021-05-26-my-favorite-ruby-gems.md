---
layout: post
title: "My favorite Ruby gems"
description: Every Ruby gem you add to a project can become a liability. The gems in this post are what I've used and trusted in the last few years.
date: 2021-05-26 16:26:23 +0200
comments: true
categories: Programming
---

I'm always hesistant when it comes to using gems. Every gem you add to a project is a bit of added risk, what if it contains a security bug? What if the developers stop maitaining it? What if it doesn't work with the next Ruby version? Of course, building everything yourself is not an option either. Through the years I've built a list of gems I trust and use. So far I've never shared these anywhere public. I'm changing that with this post.

## Authentication and authorization

- [devise](https://github.com/heartcombo/devise)

  Authentication with features like locking, forgot password, remembering sign in.

- [pundit](https://github.com/varvet/pundit)

  A much clearer manner of authorizing users when compared to cancan.

- [acts\_as\_tenant](https://github.com/ErwinM/acts_as_tenant)

  Split your application data in "tenants", which could be seperate customers, domains, etc.

## Output generation

- [redcarpet](https://github.com/vmg/redcarpet)

  Generate Markdown to HTML.

- [liquid](https://github.com/Shopify/liquid)

  A template language built by Shopify. Great for customizable webhook implementations for example.

- [blueprinter](https://github.com/procore/blueprinter)

  Fast and simple JSON serializer with a simple DSL. See my [previous post about JSON serializers](/2021/02/05/choosing-rails-json-serializer-for-your-api-in-2021/).

- [fast\_excel](https://github.com/Paxa/fast_excel)

  A very fast and simple xlsx file generator using a C library, that doesn't consume much memory.

- [caxlsx\_rails](https://github.com/caxlsx/caxlsx_rails)

  A more extensive xlsx file generatore (pure Ruby). It has more features than fast\_excel, but that comes at a cost:
  slower and more memory usage.

## Payments

- [mollie-api-ruby]()

  The official Mollie Ruby gem.

- [stripe-ruby](https://github.com/stripe/stripe-ruby)

  The official Stripe Ruby gem.

## Testing

- [mocha](https://github.com/freerange/mocha)

  Mocking and stubbing

- [hashdiff](https://github.com/liufengyun/hashdiff)

  Compare hashes and show the differences in a simple language. Great when testing JSON API responses.

- [byebug](https://github.com/deivid-rodriguez/byebug)

  Stop execution and start debugging on an interactive console.

- [capybara](https://github.com/teamcapybara/capybara)

  Test with real browsers.

# Various

- [dentaku](https://github.com/rubysolo/dentaku)

  Implement an Excel like formula system in your application. Great for giving users some computational data access.

- [cocoon](https://github.com/nathanvda/cocoon)

  Cocoon implements the frontend parts of nested forms for you.

- [roo](https://github.com/roo-rb/roo)

  Read Excelsheets, OpenDocument spreadsheets and csv files.

- [rubocop](https://github.com/rubocop/rubocop)

  Linting and other techniques to improve your code quality.

Note that I've never built a project with all these gems in it. I always try to keep the dependencies to a minimum to avoid headaches when upgrading gems or the server operating system.
