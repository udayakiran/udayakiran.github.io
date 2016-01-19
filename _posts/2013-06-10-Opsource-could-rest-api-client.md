---
layout: post
title: "Ruby - Opsource (Dimension Data) REST API client"
description: "Ruby gem to connect to op-source's REST API and perform actions without accessing the UI"
tags: [cloud, ror, ruby, web, automation]
image:
  feature: abstract-6.jpg
  color: "009688"
  icon: "clock-o"
bg_color: "009688"
---
## Problem -

We have been hosting some of our apps on the cloud provided by Op source (formally Dimension Data now.). While trying to automate a number of things with it, there was a particular scenario where we had to create a new ip and add a NAT  rule for it when a new site is created from one of our webapps. This is quite an interesting task where network and server related tasks of a cloud provider need to be automated from the web UI of another app.


## Solution -

It was quite pleasing and impressive on op source's part that they had a REST API in place for the exact need of ours. They claim that their whole web portal for network admins is built using this REST API. Such a cool design :) So, i could use their API and do the tasks i needed to. I have used the version 0.9 of the API which is the latest to the date.

### References to the API -

1. [API spec](https://github.com/udayakiran/opsource_client/raw/master/doc/Cloud-REST-API-v09-032113.pdf)

2. [API details](http://cloud.dimensiondata.com/saas-solutions/services/public-cloud/api)

### What can be done with this API ?

Well, almost everything. like

**1. Account API -** get account details, manage sub admins, list data centers and etc.

**2. Server Image API -** list and manage OS server images and customer images.

**3. Import & Export Customer Image API -** list, import and export customer images.

**4. Server API -** list the servers, deploy a server, start and shutdown a server and etc.

**5. Network API -** list networks and location, create a network and manage, manage ACLs, ips, NAT rules and etc. (This is exactly what we needed.)


**6. VIP / Load-Balancing API -** manage real servers and probes.

**7. . Files Account API -** manage file accounts.

**8. Reports API -** usage reports.


## Coding and ruby gem -

Once the impressive REST API was discoverd, it drove me enough to write a simple REST API client for opsource's API. This is written as a generic framework to support all the above mentioned APIs. As i needed to use network API, implemented network API and added calls to create and modify the NAT rule.

Source code - [Opsource client](<https://github.com/udayakiran/opsource_client>)

Install & Usage - [README](<https://github.com/udayakiran/opsource_client/blob/master/README.md>)

Please go through the README to find the usage instructions and instructions on how to add more end points.

### Moving out of singleton pattern -

Initially the gem was designed using singleton classes for the configuration as it is most likely that one organization has one opsource cloud account and singleton avoid the need to create api client objects time and again and configure them. This also prevents from wrongly configuring the credentials at diffent places. But, just for a bit of flexibility requested by a committer, i have removed the singleton restriction at some later versions.


> This is a cool design by opsource to implement their entire web and mobile UI through the APIs and expose them to the customers who wanted to drive these cloud related operations from their apps. Hope opsource_client rubygem helps acting like a starting points for any enthusiasts who want to automate things using this API.
