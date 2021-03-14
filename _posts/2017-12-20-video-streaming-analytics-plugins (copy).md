---
layout: post
title: "Video streaming - Video Streaming Analytics Using Jwplayer and Videojs"
description: "Post on how to track video streaming analytics using a couple of plugins developed for both jwplayer and videojs."
tags: [video, javascript, Web, mobile]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

Video is one of the most consumed format of content on our e-learning platform.  We were offering an inhouse developed video steaming solution that helps multiple web clients to stream videos. Our pricing model was to charge based on the amount of time spent watching the videos. We also wanted to know how many viewers are from the desktops and how many are from the mobile devices. 

<div style="text-align: center">
<figure class="full">
	<img src="/images/v3.png" width="600px" alt="">
</figure>
</div>

Hence, we ended up developing a high scaling near real time video analytics infra. In this post, I am planning to provide details of this system.

A few points to note here are -

- All our apps use either jwplayer5 or videojs as client to stream videos.
- Videos are delivered either over http / rtmp / Apple HLS based streaming methods.
- We use our own Red5 based streaming server but this method works for any streaming server as long as clients are jWplayer and videoJS.

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



## Server side - 


### Information Received By Server 

```
  { session_id: ,
    previous_position: ,
    current_position: ,
    progress: ,
    video_duration: ,
    total_session_duration:,
    additional_data: ...}
```


| Param | Explanation |
| :---- | ---- |
| session_id | A globally unique session id string that helps to identify and store data per session. Every time the video player gets launched, a new session id gets created. |
| previous_position | The position of the video controlbar when last update happend (in secs) |
| current_position | The position of the video controlbar at present (in secs) |
| progress | The overall percentage of video is watched so far (percentage |
| video_duration | Total video length (in secs) |
| total_session_duration | Total amount of time spent watched in this session (in secs.). This is culumative and calcualtes the replays, seeking back and etc. |
| additional_data | additional data initialized on client while loading the player. Can contain user specific info. |

You can use any simple http end point and write simple code to process and store these tokens. We have used a simple nodejs edge server to store these details and it was scaled uptp 20k TPS to ensure reliable, no loss progress tracking.

<div style="text-align: center">
<figure class="full">
	<img src="/images/dat.png" width="600px" alt="">
</figure>
</div>

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
