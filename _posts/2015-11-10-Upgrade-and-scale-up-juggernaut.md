---
layout: post
title: "Rails/Nodejs - Upgrade and scale up Juggernaut"
description: "Upgrade and scale up macman's juggernaut library."
tags: [ror, ruby, nodejs, websocket]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---

We used [macman's juggernaut](https://github.com/maccman/juggernaut) for realtime push notifications and chat for one of the rails apps. It was used in a 6 year old legacy app with [socket.io's](socket.io) long polling mechanism. nodejs used was of version 0.2.4. Things have changed so much in the realtime app's space since then and juggernaut is deprecated now.

We needed to upgrade juggernaut to get the following -

- We had to upgrade socket.io to a version atleast > 0.8 to solve some connectivity problems with reconnection, load balancing and to switch to websockets.

- Nodejs needed to be upgraded to as latest as possible.

- We also had to scale up the way our chat's roster script that populates list of online users. This needed some code changes and will explain this process below.

## Upgrading Juggernaut -

As macman/juggernaut repo is deprecated and is not being maintained now. So, we did a bit of research and see that we should go with - [GroupSite/juggernaut](https://github.com/Groupsite/juggernaut)

This is forked here - [udayakiran/juggernaut](https://github.com/udayakiran/juggernaut) and will be maintained from here after.

### Installation -

1) Install node https://nodejs.org/en/blog/release/v0.10.40/

2) Clone or down load the repo to a directory say “juggernaut”

{% highlight text %}

    git clone https://github.com/udayakiran/juggernaut juggernaut

{% endhighlight %}

3) Setup juggernaut -

{% highlight text %}

    cd juggernaut

    npm install

{% endhighlight %}

4) Download latest version of redis (3.0.5) and extract it. Optionally it can be installed.

5) Start redis and juggernaut

{% highlight text %}

    cd redis_src_dir

    ./redis-server

    cd juggernaut

    node server.js #nodejs server.js on Ubuntu

{% endhighlight %}

## Changes to application

- Include the application.js file in the app.

{% highlight text %}

    %script{:type => "text/javascript", :src  => "#{chat_server_url}/application.js", :charset => "utf-8"}

{% endhighlight %}


- With this clone of juggernaut, socket.io is upgraded to 0.9.9 and application.js code suggests that the way we handle channels is changed. Instead passing channel like a string, it needs to be passed like javascript object.

## Populating roster in a better way

This legacy app had it's chat built using juggernaut which needed the list of online users to be shown. This was not designed to scale. The list of online users were getting populated through periodic ajax requests to a rails metal controller which reads the data from an SQL DB. It had support for group chats, so every ajax request used to get the details of groups of the user, making the SQL queries further heavy.

Despite this being slow, it was causing huge load on app servers when number of online users are more, eventually causing scalability issues to the other parts og the app. This needs to happen though a push mechanism of juggernaut and online users need to be read from redis, rather than from a SQL database.

#### References -

      - https://github.com/Groupsite/juggernaut ('Building a roster' section)

      - http://www.ryanepp.com/blog/how-do-i-tell-if-a-user-is-online


1. Store the online users in redis. User may login from multiple tabs. So, a count is maintained to indicate the user logged in status. This counter is incremented on juggernaut connect callback and is decremented on juggernaut disconnect callback. When this count is 0, user is offline.

2. When a user record is active in redis, it should include user displayname , profile image url and groups details are stored as well. No DB queries are to be run when online user details are fetched.

3. When ever data gets updated, juggernaut event is fired to the relevant channels and the changes are pushed.

4. Need to write additional juggernaut callbacks on client to handle user coming online and going offline.

5. Also, care needs to be taken that in case redis goes down, or data is lost, it is handled gracefully.


Once this is implemented, the app started perfectly scaling up.

## Load balancing the components -

We use HAproxy as the loadbalancer. This works for all the components.

- Webscokets are loadbalanced through TCP.

- Redis can either be loadbalanced with redis sentinel and proxy like [here](https://support.pivotal.io/hc/en-us/articles/205309388-How-to-setup-HAProxy-and-Redis-Sentinel-for-automatic-failover-between-Redis-Master-and-Slave-servers) or with master-salve setup.

- Chat roster script can be run on each app server instance.

## What's next ?

Obviously, there are a number of methods to take the realtime apps forward. The roster script is not completely scalable yet as it still involves ruby. So, we can look at more concurrent options.

- Convert roster script from ruby to nodejs or something that offers more concurrency.

- We love XMPP  and erlang based [Ejabberd](https://www.ejabberd.im/) as server. We are successfully using this in a few of other apps and experienced great deal of flexibilty, cross device support and scalability. There are a number of XMPP servers out there.
