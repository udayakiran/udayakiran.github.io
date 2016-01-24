---
layout: post
title: "Ruby - Optimize the garbage collector performance (REE 1.8.7 or older)"
description: "Optimizing the GC performance of ruby to have faster and consistent rails response times."
tags: [ruby, ror, programming, performance]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

## Problem -

  It all started with a little bit of inspection into the logs where we observed that a particular rails action is randomly taking more time than expected. There were not many queries and simple view rendering was taking time. For example when 10 hits were made to the end point with no other load on the machine, every 4 hits were taking 20ms but the next hit was taking 100ms as such.

  A little more introspection revealed that a particular partial was taking that extra bit of time. Finding the root cause and fixing this was the problem.

## Analysis -

We were using New relic's monitoring and it helped in locating the issue. As there were spikes in the ruby code, it is clear that ruby's execution was taking time. Now, to get the next level details about this execution delay, we had to enable ruby's GC execution measurement. We were using ruby enterprise edition 1.8.7 and followed the link here to enable the GC monitoring - <https://docs.newrelic.com/docs/agents/ruby-agent/features/garbage-collection>

Once GC monitoring was enabled, we could easily see that every time the request took extra milli seconds, GC execution was taking that extra time, and rest remained same. So, now, we located the problem. It's ruby's garbage collector!

## Solution -

A little bit of search on how to optimize ruby GC helped me to find the reference from [REE's documentation](http://www.rubyenterpriseedition.com/documentation.html#_garbage_collector_performance_tuning)

### Tuning the GC -

We use passenger as our app server. We need to find out the optimal heap settings for ruby and configure passenger to run with this GC tuned ruby.

#### A. Observe the heap stats -

Observe the heap usage on the specific app server which you need to optimize (for production, examining one app server is enough if all your app servers are identical.)

Install gdb.rb to print the ruby process related stats prettily.

{% highlight ruby %}

Install gdb.rb:
sudo gem install gdb.rb

{% endhighlight %}

Use `sudo passenger-status` to find a thread that has handled enough requests and note its PID.
Connect to the passenger thread with `gdb.rb`:

{% highlight ruby %}

sudo gdb.rb <pid>

{% endhighlight %}

Get `gdb.rb` to print out the stats about your objects:

{% highlight ruby %}
ruby objects

You will find a section that looks like below:

  HEAPS            6
  SLOTS      2435789
  LIVE       1159435 (47.60%)
  FREE       1266614 (52.40%)

{% endhighlight %}

We're going to assume that "LIVE" is the approximate number of slots you normally use up. Round that up to something like 1,500,000 and calculate the below.

{% highlight ruby %}

RUBY_HEAP_MIN_SLOTS=1800000          # Slots Live + 20%
RUBY_HEAP_FREE_MIN=18000             # 1% of HEAP_MIN_SLOTS
RUBY_HEAP_SLOTS_INCREMENT=144000     # 8% of HEAP_MIN_SLOTS
RUBY_HEAP_SLOTS_GROWTH_FACTOR=1
RUBY_GC_MALLOC_LIMIT=60000000

{% endhighlight %}

These settings can be tweaked as you like. These are the settings that worked for me and for our app. They can be tweaked as needed. All we are trying to do here  is to allocate adequate heap space to minimize the GC's efforts.

#### B. Export these settings for ruby executable

Create a wrapper script that sets these variables in the environment before calling ruby. For example i ll create a file `ruby_gc_tuned` in /usr/local/bin and add the below lines.

{% highlight ruby %}
#!/bin/bash

export RUBY_HEAP_MIN_SLOTS=1800000
export RUBY_HEAP_FREE_MIN=18000
export RUBY_HEAP_SLOTS_INCREMENT=144000
export RUBY_HEAP_SLOTS_GROWTH_FACTOR=1
export RUBY_GC_MALLOC_LIMIT=60000000

exec "/usr/local/bin/ruby" "$@"

{% endhighlight %}

#### C. Edit the ruby path in passenger config

Edit passenger.conf and change the PassengerRuby value to point to ruby_gc_tuned.

{% highlight ruby %}

PassengerRoot /usr/local/lib/ruby/gems/1.8/gems/passenger-3.0.11
PassengerRuby /usr/local/bin/ruby_gc_tuned

{% endhighlight %}

Now restart apache and check NewRelic to see how you did.

## Improvements Observed -

In our case the 100ms taken by the requests on and off has dropped to 35ms. The 80ms taken by ruby GC went down to 15ms.

This remained very much constant.

## Future -

This is a note that this particular optimization may not be needed any more after ruby 2.0's release. So, if you are running on ruby 2.0 (with YARV) you are good to use the ruby as such as heap size optimization is not required.
