---
title: Ejabberd - Issues faced and tips
date: 2015-10-02 00:00:00 -04:00
tags:
- xmpp
- web
- programming
layout: post
description: Ejabberd - Issues faced while developing a scalable XMPP chat and tips
  to solve this
image:
  feature: abstract-6.jpg
  color: '616161'
  icon: clock-o
bg_color: '616161'
---

This post mentions some of the issues we faced while implementing XMPP chat with ejabberd server and solutions for it. Our's is a rails app that uses ejabberd as chat server.

<div style="text-align: center">
<figure class="full">
	<img src="/images/eb.png" width="600px" alt="">
</figure>
</div>

## 1) User registration from our app -

Our requirement is that when a new user signs up to our app, a new ejabberd account needs to be created. Obviously this is the same case with many of the apps. We used ruby' XMPP client for this. We were seeing an error that users could not be created as the limit for the number of users reached.

The reason is that ejabberd by default has a limit that only x number of users can be registered every 10 mins. This is configurable.

### Fix -

Edit the ejabberd config file (a yml file and in our case it is at - `/opt/ejabberd-15.04/conf/ejabberd.yml`) and set registration_timeout to needed value. As we did not want any limit here we had set it to `infinity` .

{% highlight text %}
# around line 481 for ejabberd-15.504 - under 'register' stanza

register:
   all: allow
   registration_timeout: infinity

# around line 494 - top level stanza
registration_timeout: infinity

{% endhighlight %}

## 2) Avoid websocket timeout -

We used websockets for the users to connect to ejabberd and looks like ejabberd treats the websocket connection as idle if there is no activity for 5 mins and terminates the connections. So, idle users were getting disconnected. To prevent this, we chose to enable mod_ping and made sure the connections do not get terminated.

### Enabling mod_ping -

In ejabberd.yml

{% highlight text %}

mod_ping:
    send_pings: true
    ping_interval: 250 # default value is 32 secs. 4.5 mins ll do for us.
    timeout_action: none

{% endhighlight %}

More about mod_ping - <http://docs.ejabberd.im/admin/guide/configuration/#modping>

## 3) Creating a global shared roster -

We wanted every user in the app to be able to see every other user. There are group chats but they are implemented through chat rooms. This means every user is in the contacts of every other user. So, we decided not to create roster list for each user (which is obviously not smart) and instead created a global shared roster like explained below.

1. Access ejabberd admin interface on browser - http://yourhost:5280/admin

2. On the left navigation panel, choose Virtual hosts > yourhost > Shared Roster Groups.

3. Create one with name 'everyone' members value as '@all' and displayed groups as 'everyone'. (Note - 'everyone' is just a sample name. Use your desired name.). It looks like the screenshot below -

<figure class="full">
	<img src="/images/shared_roster_all.png" alt="">
	<figcaption style="text-align: center">Shared global roster creation</figcaption>
</figure>

Learn more about shared roster here - <http://docs.ejabberd.im/admin/guide/configuration/#modsharedroster>

## References -

Ejabberd Documentation - <http://docs.ejabberd.im/>

Ejabberd Configuration - <http://docs.ejabberd.im/admin/guide/configuration/>
