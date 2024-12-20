---
layout: post
title: "Choosing a Rails JSON serializer for your API in 2021"
description: "There are a lot of Rails JSON serializers, but not all of them are well maintained. Find out which ones are fast and are still maintained."
date: 2021-02-05 14:17:12 +0100
comments: true
categories: Programming
---

The state of JSON serialization in the Rails world seems to change fast and often. A few years back most developers advised you to use [ActiveModelSerializers](https://github.com/rails-api/active_model_serializers) if you cared about speed, but most of them have since considered the project dead because the last releases only seem to be maintenance, while the master branch hasn't been touched since 2015. Furthermore it seems Netflix stopped maintaining the [Fast JSON API](https://github.com/Netflix/fast_jsonapi) gem while the [RABL](https://github.com/nesquena/rabl) gem hasn't seen any releases since 2018. So what would I pick when building a new API in Ruby on Rails in 2021?

## Jbuilder
On of the most common known gems to serialize objects into JSON is probably Jbuilder. Developed by the authors of Rails and it is even mentioned in a Gemfile comment for new Rails projects. Last release at the time of this writing was in September 2020. Serialization is configured in views with a simple but flexible DSL. You can generate any JSON structure you like using this gem. For simple API's this works fine while rendering speed still seems to be ok. All in all a solid choice for a new API that doesn't have too much data or users yet. Find out more about it on [their Github](https://github.com/rails/jbuilder) page.

## JSON:API Serializer
A fork of the original Fast JSON API project that was started by Netflix. When they stopped maintaining it some community members stepped up and continued the project under this name. If you want to conform to the JSON:API specification and care about speed, this is probably your most solid choice. Last release at the time of this writing was in August 2020. Find out more about it on [their Github](https://github.com/jsonapi-serializer/jsonapi-serializer) page.

## Blueprinter
A newcomer to the scene! It's always great when people step up to fill a gap. This is my personal favorite because it gives you the nice DSL with serializers (Blueprints) that I've known from ActiveModelSerializers and Fast JSON API, while allowing you to render any JSON structure without giving up speed. If you expect your API to see lots of traffic you should definitely consider using this gem. Last release at the time of this writing was in November 2020. Find out more about it on [their Github](https://github.com/procore/blueprinter) page.

## Summary
Based on my research and experience so far, I prefer Blueprinter for JSON serializing most of the time.
