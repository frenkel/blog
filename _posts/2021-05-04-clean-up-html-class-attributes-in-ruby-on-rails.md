---
layout: post
title: "Clean up HTML class attributes in Ruby on Rails"
date: 2021-05-04 14:23:12 +0200
comments: true
categories: Programming
---

I keep on discovering handy view helpers in Ruby on Rails while developing [Callcounter](https://callcounter.eu). A few weeks back I remembed [cycle](https://api.rubyonrails.org/classes/ActionView/Helpers/TextHelper.html#method-i-cycle) and last week I discovered a new helper that was introduced in Ruby on Rails 6.1: [`class_names`](https://api.rubyonrails.org/classes/ActionView/Helpers/TagHelper.html#method-i-class_names).

## Beautify your views

Most of us will probably recognize the class name spaghetti that starts to arise when your project grows. Things like this will become littered throughout your views:

```
<li class="item <%= 'active' if @active %>
    <%= 'disabled' if @unpaid_user %>">
```

Not exactly readable anymore, right? Well, thats what `class_names` is trying to fix. You just pass it a hash with the class names as keys and conditions as values. Look how nice!

```ruby
<li class="<%= classs_name item: 1, active: @active, disabled: @unpaid_user ">
```

You sometimes even need an inline ternary operator:

```
<li class="<%= @verified_user ? 'verified' : 'unverified' %>">
```

This can be cleaned up as well:

```
<li class="<%= class_names verified: @verified, unverified: !@verified %>">
```

A final improvement might be done by using the `tag` helper:

```ruby
tag.li class: class_names(verified: @verified, unverified: !@verified) do
  # content
end
```

## What if your project uses an older Ruby on Rails version?

The great thing about these helpers is that they are so simple that you can easly backport them to older releases yourself. Something like this in `app/helpers/class_names_helper.rb` should work on older releases:

```ruby
module ClassNamesHelper
  def build_tag_values(*args)
    tag_values = []

    args.each do |tag_value|
      case tag_value
      when Hash
        tag_value.each do |key, val|
          tag_values << key.to_s if val && key.present?
        end
      when Array
        tag_values.concat build_tag_values(*tag_value)
      else
        tag_values << tag_value.to_s if tag_value.present?
      end
    end

    tag_values
  end

  def class_names(*args)
    tokens = build_tag_values(*args).flat_map { |value| value.to_s.split(/\s+/) }.uniq

    safe_join(tokens, " ")
  end
end
```

## Discussion

Let me know if you found this post useful!
