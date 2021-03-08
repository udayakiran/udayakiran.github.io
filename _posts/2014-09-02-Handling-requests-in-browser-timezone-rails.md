---
layout: post
title: "Handling requests in browser time zone in a rails app"
description: "Handling requests in browser time zone in a rails app"
tags: [javascript, programming, ror, ruby, web]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---
When you are building a web app that involves dealing with a lot of time related information and presenting it to the user, you would like to show the time information in user's time zone so users don't have to do the timezone conversions.

<div style="text-align: center">
<figure class="full">
	<img src="/images/tz0.png" width="600px" alt="">
</figure>
</div>

In this post, i'll try to solve this problem keeping Ruby on Rails as my web app framework. The approach would be same for any webapp except the change in code and syntax.

The most seamless way of showing time information in the user's time zone is to track the time zone from the browser and run the time related operations on your server considering this time zone and return the time in this time zone. As simple as that.

## Common solutions -

Let's look at some common methods we can use with ROR -

As Eli has nicely written these up here - <https://viget.com/extend/using-time-zones-with-rails> , METHOD -1 has the short coming of not being able to detect the Day light savings METHOD -2 of JSTZ is preferred. This works 90% of the times but there is no guarantee that this solution works with any server side framework all the time.

The main reason is jstz determines the time zone and returns it as a *String*. There is no standard in the strings used by the software to represent the time zones unfortunately and due to this some of the cases fail even with Rails.

Just to confirm - please go you rails console and print the following.

{% highlight css %}

ActiveSupport::TimeZone::MAPPING
ActiveSupport::TimeZone::MAPPING.keys
ActiveSupport::TimeZone::MAPPING.values

{% endhighlight %}

You will observe that these are not the same string used by jstz if you can look at it's time zone.

Hence, this solution does not work for all the cases as well. Also, it is observed that Rails keep adding support for new time zones as they are adopted by the cities / governments. Changing the strings of jstz to be same as Rails's is one approach but i am not recommending that.

## My approach -


My approach to solve this problem is purely based on the offsets. Because -

* Offsets are the standard across the time zones unlike name, so we only pass the offset values to server let Rails / any server software decide the time zone name.

 * By tracking summer and winter offsets we can handle the daly light savings issues.

 * Another point to handle is the changes to the time zones and their adoption by the software -
Cities and governments can always choose to change a time zone or apply changes to their day light savings.  For example, Samoa was in SST (UTC - 11hrs) till December, 2011 but they switched their time zone later to WST (UTC + 13hrs).
(Ref - <http://www.timetemperature.com/pacific/samoa_time_zone.shtml>).  These changes might / might not have been picked up by user's browser or the server software (Ruby / Rails in this case). We do not have control over the browser but we should be able to decide a baseline year from when we are considering the time zone changes.


## Final solution -

I have put together my approach as a gem (that works for rails as of now but can easily be extended to others.) -

{% highlight html %}

https://github.com/udayakiran/rails_browser_timezone

{% endhighlight %}

This is tested for rails 2.3.x, 3.x and 4.x and works fine for us.

Please follow the steps in README to use it in your app.

## Open Issue -


 Browsers some time do not keep them up to date with the time zone changes and they are buggy.

For example, as i am writing this, Google Chrome sends the offsets of Samoa time zone as WST for all the dates before and after 2011 which is an issue. Firefox sends the time zone offsets as SST for both the dates before and after 2011, which is also incorrect.

However, rails 4.x (ruby 2.2) knows that Samoa before 2011, December is SST and  WST after that.

But, this is one of those edge cases. For the popular time zones browsers and rails does a very good job and the solution works.

## Conclusion -

The approach i used worked for us in majority of the cases by choosing the correct baseline year. Only point to not is that Rails 2.x and 3.x might not be able to track the time zone changes that happened after their year. But these are <2% edge cases as we observed. But, the rest worked well.

Please feel free to be touch about any issues faced / bugs reported through the github page of the gem.

> I would say "Time zones are some times complex as they change and there is a difference in the adoption across the browsers. But, majority of the time zones we have traffic from, are simple !"
