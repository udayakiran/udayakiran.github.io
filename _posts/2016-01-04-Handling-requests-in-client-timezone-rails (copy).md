---
title: TimeZone - Handling requests in client's time zone in a rails app
date: 2016-01-04 00:00:00 -05:00
tags:
- javascript
- programming
- ror
- ruby
- web
layout: post
description: Handling requests in the client's time zone in a rails app, based on
  the request.
image:
  feature: abstract-6.jpg
  color: '616161'
  icon: clock-o
bg_color: '616161'
---

This post is a continuation of one of my previous posts -

[TimeZone - Handling requests in client's time zone in a rails app]({% post_url 2014-09-02-Handling-requests-in-browser-timezone-rails %})

It is recommended to visit that post before proceeding furthur on current post.

<div style="text-align: center">
<figure class="full">
	<img src="/images/tz.png" width="600px" alt="">
</figure>
</div>

This post describes an enhanced solution of rails_browser_timezone gem.

## Open issues with rails_browser_timezone -

1. The very first hit to the server from a browser does not pass the browser offsets, which means this request runs in either the default system timezone or the last known timezone from the DB.

2. This method does not help when the requests are received through APIs. APIs need to either explicitly pass browser off sets with each request or the requests run in the last known timezone which is persisted.

3. Some browsers take time to reflect upon the new timezone when client's system time zone is changed. So, those few requests made meanwhile do not have the updated timezone.

## Alternatives -

While looking at some alternatives to the previous approach all i could find was either to go with JS based timezone tracking or tracking the timezone based on the geo-location which can be obtained from the request's IP address.

JS based timezone tracking is buggy when it comes to handling the time zone names on rails servers, as we know from the previous post. Though this can be fixed by mapping these time zones to rails's timezone strings, we still have the problem that APIs cant use this method.

Hence, tracking the timezone based on geoip seems to be one good alternative. The only limitation of this approach is that, a user who has his system timezone different than his location's timezone will still see the information in the location's timezone.

This is just a decision based on your app and how you want to deal with it. So, wanted to write a gem with supports timezone tracking based on both browsers and geoip and leave the developers with the flexibility of deciding which method they want to use to choose this.

## A comprehensive solution -

Keeping the above discussion up, tried to put together a gem called `rails_client_timezone` which intends to solve all the above mentioned problems and gives developers the flexibility to choose how they want to track the time zone.

Source - <https://github.com/udayakiran/rails_client_timezone>

Please follow the README which helps to get started.

- This gem reuses the logic from [rails_browser_timezone gem](https://github.com/udayakiran/rails_browser_timezone) to track browser based timezones.

- It can track the timezone based on the ip with the help of [geoip gem](https://rubygems.org/gems/geoip/versions/1.6.1). A few tweaks were needed to this gem and had to put in efforts to map some of these timezone strings to match with the rails's timezone strings.

- This gem works smartly to track the timezone from ip if browser offsets are not present and it also lets the programmers set the needed preference. This is a key addition.

### Explanation for modes -

This gem supports 3 modes which can optionally be configured by the developers. Default mode is `:smart` .  Blow is the explanation for modes.

**:ip -** Time zone will be detected based on the request's ip address(using geoip gem's logic)

**:browser -** Time zone will be detected based on browser utc offsets.

**:smart -** Time zone will be detected by browser if offsets are set or it falls back to ip(:browser mode first, which falls back to :ip mode).


Create a file in your initializers and set the 'mode' to your choice.

{% highlight ruby %}

# Say in config/initializers/rails_client_tz_init.rb

RailsClientTimezone::Setting.mode = :ip
#default value is :smart. Accepted values - :browser, :ip, :smart

{% endhighlight %}

### Keeping the geoip data upto date -

This is one minor limitation / update i think we will have to deal with while using this gem. This is needed only for `:ip` and `:smart` modes.

Geoip gem depends on geo data which consists of the information about the ips mapped to the geo locations. This database is consistent and up to date as of now, but in future to improve it's accuracy and bring in the changes, we can update this any time. There are a number of websites which provide this data.

By default Geoip City db file is available in the data directory, to override that db file you can download it from Download geoip city database and place anywhere in your app. Create a file in your initializers and set the geo ip city db file path. This step is optional if you are good with the data provided by the gem.

{% highlight ruby %}

# Say in config/initializers/rails_client_tz_init.rb

RailsClientTimezone::Setting.geoip_data_path = <file_path>  #Default path is <gem_source>/data/geoip/GeoLiteCity.dat

{% endhighlight %}

>> Hope that this gem provides needed help for the rails developers in handling the issues with time zones.
