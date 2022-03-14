---
title: Scalable Realtime Chat (Text, Audio, Video) - using XMPP
date: 2016-02-23 00:00:00 -05:00
tags:
- java
- Browsers
- Web
- Java web start
- HTML5
layout: post
description: Scalable Realtime Chat (Text, Audio, Video) - using XMPP
image:
  feature: abstract-6.jpg
  color: '616161'
  icon: clock-o
bg_color: '616161'
---

## Problem -

I got a chance to work on multiple asych real time applications on the web early in my career. Being part of an e-learning product cloud demanded us to build high scale real time chat use cases for collaborative learning experience. These applications were running on desktop browsers, mobile/tablet browsers and on android/iOS native apps.

<div style="text-align: center">
<figure class="full">
	<img src="/images/chat.jpg" width="600px" alt="">
</figure>
</div>

To deliver a simple chat is easy but when you try doing it at scale and evolve its architecture to make it reliable taught me many interesting learnings. Some of the challenges include - 

- Roster management to show who of my contacts are online.
- Deliver real time chat messages , including media content.
- Maintain high concurrency for all operations.
- Chat history management.
- Notifications.
- Handling chat events across multiple tabs/browsers and devices. Synchronize them.
- Blocking calls from other contacts if user's call is active.
- Handle hardware usage diligently call has ended.
- Group chats and group calls
- Cost effective design

## Solution -



<div style="text-align: center"><iframe src="//www.slideshare.net/slideshow/embed_code/key/fYvQrGAiRvuXz8" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/udayslideshare/scalable-real-time-chat-text-audio-video-implemented-using-xmpp" title="Scalable Real Time Chat (Text, Audio, Video) - Implemented using XMPP" target="_blank">Scalable Real Time Chat (Text, Audio, Video) - Implemented using XMPP</a> </strong> from <strong><a href="https://www.slideshare.net/udayslideshare" target="_blank">Udaya Kiran</a></strong> </div></div>

## Results

We could achive 800k connects per server on Ejabberd with 8 GB primary memory. Successfully Scaled up entire chat system to meet low latency text, audio and video chat needs. 

## References

- XMPP and WebSocket - http://stackoverflow.com/a/26560860, https://blog.andyet.com/2014/10/30/websocket/
- XMPP over Socket.io - http://stackoverflow.com/a/33868081
- Jingle - http://xmpp.org/extensions/xep-0166.pdf
- XMPP fundamental stanza examples - [http://xmpp.org/rfcs/rfc3921.html#stanzas-presence-children-show](http://xmpp.org/rfcs/rfc3921.html)
- BOSH vs WebSockets - http://stackoverflow.com/a/6442488
- XMPP and WebRTC - https://xmpp.org/uses/webrtc.html
- Lua vs Erlang - http://vschart.com/compare/lua/vs/erlang-programming-language

