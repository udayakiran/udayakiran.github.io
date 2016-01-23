---
layout: post
title: "Video streaming - Track video streaming analytics using jwplayer and videojs"
description: "Post on how to track video streaming analytics using a couple of plugins developed for both jwplayer and videojs."
tags: [video, javascript, web, mobile]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

As part of one of our products, we were offering a video steaming solution that helps multiple web apps to stream videos. We wanted to charge for video streaming based on the amount of time spent watching the videos and also wanted to know how many viewers are from the desktops and how many are from the mobile devices. So, will explain below how to build something that tracks all this basic information.

A few points to note here are -

- All our apps use either jwplayer5 or videojs to stream videos.

- The streaming server can be either red5 or wowza or amazon cloud front.  

## Options to track video analytics -

We can track this information in one of the following ways -

### a) Through Video player (Recommended) -

We can write a jwplayer plugin for desktops and videojs plugin for mobiles which will send the amount of video watched by user.

On server, this data can be written either directly to DB after processing or first to a store like redis/memcached and then to the database.

#### Advantages -

1. This keeps video tracking logic generic and app independent. Same plugin works for all apps and all streaming servers. No maintenance is needed if we switch streaming servers.

2. Very loosely coupled and same code works for both mobiles and desktops.

3. Can be easily extended to track more info as needed.

### b) Through steaming server (Not Recommended)

We need to write an app for the streaming server (red5/wowza/nginx-rtmp) which tracks it based on the client/connection. Paid streaming services like wowza and AWS cloud front provide some of these stats out of the box but others do not. This data needs to be exposed to app servers so that they can access it and store in their database. Streaming server can also push the data.

#### Disadvantages -

1. Complex to build. Need to build the red5/wowza apps and also a way to store data locally and then push/expose it to the web apps.

2. Not maintainable. We need to write different apps if we need to move to another media server.


## Implementation -

Wrote two plugins for jwplayer and videojs each using their JS APIs. The plugins can track the below information session by session. This can be reported like JSON to the server end point URL that is configured.

- Progress

- Time spent on the video in any session

- Video duration

- Browser/Device (not included in params. Just read “user-agent” header of each request)

- Number of attempts

- Pass any additional data during initialzation so that it can be sent to the server along with the updates.

- Also, lets you resume from the video from the last left point if you choose to.

Below is the source code of the plugins and usage instructions.

### For Jwplayer -


Plugin name - jwplayer-tracker

Source - <https://github.com/udayakiran/jwplayer-tracker>

Follow the README to find the information about usage, config params and tips.

### For VideoJs -

Plugin name - videojs-tracker

Source - <https://github.com/udayakiran/videojs-tracker>

Follow the README to find the information about usage, config params and tips.

## Applications of the tracked analytics -

Though the plugins send data in the raw format, following information can be tracked by using this effectively.

1. Number of users on each devise.

2. Number of users by location.

3. Amount of time spent on the video.

4. Number of people who completely watch the video.

5. All the above information can be tracked over period of time.

Below is a simple image showing how the tracked data can be presented.


<figure class="full">
	<img src="/images/jwplayer-streaming.png" alt="">
	<figcaption style="text-align: center">Original figure taken from jwplayer.com</figcaption>
</figure>
