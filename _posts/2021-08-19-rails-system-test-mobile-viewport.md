---
layout: post
title: "Rails system test with mobile viewport"
description: "It is possible to write system tests with different viewport sizes, allowing you to test both mobile and desktop renders of the same page"
date: 2021-08-19 13:25:19 +02:00
comments: true
categories: Programming
---

While building my subscription tracking service I broke the mobile navigation menu and deployed it to production. It was only after a day or so that a user emailed me to report this bug. I directly understood why my ads did not convert! This should never happen again, let's create a system test with mobile viewport sizes that verifies the menu works correctly.

## Default screen size desktop

As you might know, the default Rails system tests use dimensions that are defined in `test/application_system_test_case.rb` with a line such as:

`driven_by :selenium, using: :headless_chrome, screen_size: [1400, 1400]`

The most simple solution would be to just modify the sizes in that array. However, this would make all system test cases use the mobile viewport, which is not what I want.

## Every test case a different screen size

After some searching I found that the Rails APIs did not support setting the screen size for one test case. Capybara, which is used as an underlying gem, does however. So as the first line to a mobile viewport test case you can set the screen size using:

`Capybara.current_session.current_window.resize_to(360, 740) # Galaxy S9`

The naive solution to resetting the screen size after this test case would be to repeat this call with the original 1400, 1400 as arguments. However, if the test does not succeed, it will not execute that line. It is therefore better to reset the viewport in a seperate teardown method, for example in your `test/application_system_test_case.rb` file:

```
teardown do
  Capybara.current_session.current_window.resize_to(1400, 1400)
end
```

You can DRY the resulting `test/application_system_test_case.rb` a bit by storing the default size in a const array and using that in the various calls. The one I use now looks like this:

```
# frozen_string_literal: true

require 'test_helper'

class ApplicationSystemTestCase < ActionDispatch::SystemTestCase
  WINDOW_SIZE = [1400, 1400].freeze
  driven_by :selenium, using: :headless_chrome, screen_size: WINDOW_SIZE

  teardown do
    Capybara.current_session.current_window.resize_to(*WINDOW_SIZE)
  end
end

```

[Subscribe to the RSS feed](/feed/) to be notified of my next blog post!
