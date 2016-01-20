---
layout: post
title: "Ruby/Rails - Capistrano 3 - SVN support"
description: "Support SVN as SCM for capistrano 3 deployments"
tags: [javascript, programming, web, js library]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---

## Why ?

Well, Capistrano 3 has dropped the support for SVN as source control mechanism. Unable to to implement this in a generic way was the reason quoted. Discussion can be followed on the github issue here - <https://github.com/capistrano/capistrano/issues/752>

Looks like there are no plans to commit this fix to the branch any time soon and SVN is no more a priority for capistrano. So, i have put together my fix (not very pretty though..) to support SVN and like to share it in case it helps.

## Solution -

Install capistrano gem from the source here -

<https://github.com/udayakiran/capistrano/tree/3.4.0-svn-scm>

This fix is currently made on 3.4.0 on a fresh branch and i am not planning to merge this with trunk any time just to keep this fix a separate one. Just go through the commit history to see the changes made. These changes can be easily applied to later versions of capistrano.


### Installation instructions -

Same as installing a gem form any git branch.

A) Add the below line to your Gemfile if you are using one.

{% highlight ruby %}

gem 'rails', :git => "git://github.com/udayakiran/capistrano.git", :branch => "3.4.0-svn-scm"

{% endhighlight %}

OR

B) Follow the steps in [this stackoverflow answer](http://stackoverflow.com/questions/2823492/install-gem-from-github-branch) to build the gem.
