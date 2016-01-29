---
layout: post
title:  "Setup Trouble with CarrierWave and Fog"
date: 2016-01-29
categories: code
author_name : Dave Moore
author_url : /about
author_avatar: dave
show_avatar : false
read_time : 5
feature_image: feature/landscape-007
show_related_posts: false
square_related: recommend-wolf
---

Today I was configuring a new install of CarrierWave to use S3 storage via the
Fog-AWS gem and hit a snag. After following the docs in the Carrierwave readme,
I kept getting no method errors on the fog_provider portion of the config.

Here's the trick, RubyGems links to the 0.10.0 version while GitHub shows
master. Instead of referring to the master docs, be sure you look over the 0.10.0
readme:

CarrierWave 0.10.0
Fog >= 1.3.1

{% highlight ruby %}
CarrierWave.configure do |config|
  config.fog_credentials = {
    :provider               => 'AWS',                        # required
    :aws_access_key_id      => 'xxx',                        # required
    :aws_secret_access_key  => 'yyy',                        # required
    :region                 => 'eu-west-1',                  # optional, defaults to 'us-east-1'
    :host                   => 's3.example.com',             # optional, defaults to nil
    :endpoint               => 'https://s3.example.com:8080' # optional, defaults to nil
  }
  config.fog_directory  = 'name_of_directory'                     # required
  config.fog_public     = false                                   # optional, defaults to true
  config.fog_attributes = {'Cache-Control'=>'max-age=315576000'}  # optional, defaults to {}
end
{% endhighlight %}

The moral if the story friends is to always double check your version and refer
to the correct docs!

Cheers!
