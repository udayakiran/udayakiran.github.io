---
layout: post
title: "Scalability - Time to relook at you distributed file system."
description: "Look at the performance of your DFS and see which is the option that suits"
tags: [web, performance, scalability]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---

This is a post explaining how we realized our scalability bottle necks and considered the alternatives for our distributed file system.

We strongly follow the distributed architecture and try to scale out each of our components as much as possible. At the same time, care is taken that things are not scaled up prematurely but they are done as we go in an incremental fashion. One such components of us was the distributed file system.

## Problem -

We wanted to save some static assets and videos from our app servers on to a content server through a mounted drive which is mounted using [GlusterFS](https://www.gluster.org/). Our files can be small text files, images and etc. plus videos that can be of size upto 3-4 GBs. We wanted to use glusterfs for a number of reasons and easy to mount and manage is one of those. Things went very well for more than a year and we had collected close to 100GB data on production. Suddenly we were seeing issues like slow response times, especially with large video uploads. It reached a state where a video of size 3 GB was taking 2-3 mins time to get written to the disk.

## Analysis & Options -

Looking more at the details we found that our dfs was the real bottleneck. A simple file copy was taking close to 2 mins to write the file to the hard disk. A few things we did and wanted to do were -

 - Move to faster SSD hard disks.

 - Switch from our 1 gbps network to a faster one.

 - Either optimize or consider alternatives for the dfs.

First two changes are infrastructure related but the third one needed some real research into. A few performance optimizations did not help us much and we considered some alternatives. Below presentation titled ['Performance comparison of Distributed File Systems on 1Gbit networks'](http://www.slideshare.net/azilian/performance-comparison) gives some insights.

<iframe src="//www.slideshare.net/slideshow/embed_code/key/bqytUCI2lOC2QY" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/azilian/performance-comparison" title="Performance comparison of Distributed File Systems on 1Gbit networks" target="_blank">Performance comparison of Distributed File Systems on 1Gbit networks</a> </strong> from <strong><a href="//www.slideshare.net/azilian" target="_blank">Marian Marinov</a></strong> </div>

### Decision -

- After a bit of research we wanted to move to Hadoop DFS as we needed good speeds for both small and large files and we wanted to have a truly distributed system.

- We wanted this solution to be like a mounted file system. So, went ahead with mapr's implementation.

The next thing is to see if this really does the needed job, and i m writing down a few speed tests that show this.

## Performance testing with HDFS -

Showing the file copy speeds from local machine to HDFS drive and vice versa that indicate the improvements.

**Using cp command from Local to HDFS -**

|File size| Machine| Start time | End time |Remarks|

|Small file (mention size 50 MB)| 10.229.94.18| |  | < 1Sec |
|Medium file (mention size 615 Mb)| 10.229.94.18| 07:52:20  |  07:52:23 | 3 secs |
|Large file (mention size 1.1GB) |10.229.94.18 | 07:55:18 |07:55:24  | 6 secs |
|Very large file (mention size 2.4 GB)| 10.229.94.18| 07:46:52  | 07:47:14  | 22 secs | |


**Using cp command from HDFS to Local -**

|File size| Machine| Start time | End time |Remarks|

|Small file (mention size 50 MB)| 10.229.94.18| | |  < 1Sec |
|Medium file (mention size 615 Mb)|10.229.94.18 |08:05:39 | 08:05:41| 2 secs |
|Large file (mention size 1.1GB ) | 10.229.94.18|08:02:52 | 08:02:56| 4 secs |
|Very large file (mention size 2.4 GB)| 10.229.94.18|  07:58:20 | 07:58:37| 17 secs | |

We can clearly see that a 2.4 GB file is taking about 20 secs of time compared to 2 mins with glusterfs. So, it is clear and we went ahead with HDFS.

## Conclusion -

>> There are a number of DFS solutions out there and the one that suits you is the one to start off easily and lets you optimized later. Gluster helped us to get started fast and run smoothly for a year's time. Once we hit more than a few hundred gbs of data and started seeing the problems, we just switched to HDFS.
