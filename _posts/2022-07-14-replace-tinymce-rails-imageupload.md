---
layout: post
title: "Replace tinymce-rails-imageupload"
description: "tinymce-rails-imageupload has been discontinued and it will keep your project on TinyMCE 4 forever.
Use these steps to replace it and upgrade to TinyMCE 6."
date: 2022-07-14 16:02:28 +02:00
---

I maintain a number of Ruby on Rails projects that contain the great 
[tinymce-rails-imageupload gem](https://github.com/PerfectlyNormal/tinymce-rails-imageupload).
Unfortunately the owner has archived the repository and is no longer maintaining it. This was keeping my projects on the
rather old TinyMCE version 4. Last week I've invested some time in search of a solution and I found a good one that
does not rely on external dependencies!

Start by removing `tinymce-rails-imageupload` from your `Gemfile` and upgrading `tinymce-rails` to version 6.1.
Make sure you upgrade your `tinymce.yml` file with the renamed 6.1 plugins and options before you continue.
Test whether TinyMCE still works without the image uploads.

Now **replace** the `uploadimage` toolbar button with `image` and the `uploadimage` plugin with `image` in your
`tinymce.yml` configuration file and **add** these two options:
```
  images_upload_url: '/tinymce_assets' # for automatic_uploads
  images_upload_credentials: true # sends session information with the upload
```

To avoid some confusion this is the minimum viable tinymce.yml configuration file:
```
default:
  toolbar:
    - image
  plugins:
    - image
  images_upload_url: '/tinymce_assets' # for automatic_uploads
  images_upload_credentials: true # sends session information with the upload
```


Note that `/tinymce_assets` was the default endpoint for `tinymce-rails-imageupload` POST requests. That controller action
will need a small modification as well. The previous situation was probably something like this:

```
render json: {
  image: {
    url: the_url_of_the_upload_here
  }
}, content_type: 'text/html'
```

Replace it with a different JSON object and a normal content type:

```
render json: { location: the_url_of_the_upload_here }
```

That's it, you should now have a nice image upload tab when you click the image button on the toolbar.
As a bonus TinyMCE now also supports dragging an image into the editor which will use this endpoint to
store it on the server!

[Follow me on twitter](https://twitter.com/frankgroeneveld) or [subscribe to the RSS feed](/feed/) to be notified of my next blog post!
