---
layout: post
title: "File upload progress bar with apache's progress upload module"
description: "File upload progress bar with apache's progress upload module."
tags: [web, programming]
image:
  feature: abstract-6.jpg
  color: "009688"
  icon: "clock-o"
bg_color: "009688"
---

## Problem -

  Build a simple file upload progress bar for a  web app (ruby on rails app running on apache with pushion passenger).

## Implementation -

The file upload progress bar can be implemented using the Upload progress module for apache <https://github.com/drogus/apache-upload-progress-module>.

### Installation & Configuration -

1) Download the source code

```
    wget https://github.com/drogus/apache-upload-progress-module.git
```

Alternate source: `wget --no-check-certificate`

```
    http://github.com/drogus/apache-upload-progress-module/tarball/master
```

2) Compile the source code and install the module in apache

```
    cd apache-upload-progress-module
```

```
    sudo apxs2 -c -i -a mod_upload_progress.c
```

**Note -** Please note that to compile the module, you will need threaded development library of apache2

3) Modify apache configuration

a) In apache conf, load the file upload module

    {% highlight c %}
    LoadModule upload_progress_module libexec/apache2/mod_upload_progress.so
    {% endhighlight %}

b) In the VirtualHost configuration of the application add

    {% highlight c %}

        <Location />
          # enable tracking uploads in /
          TrackUploads On
        </Location>

        <Location /progress>
          # enable upload progress reports in /progress
          ReportUploads On
        </Location>
      {% endhighlight %}

4) Restart the apache server.

### Code changes in the app -

- In the file upload form action url, append `X-ProgressID=<GUID>`.
 (make sure that this is the last key-value in the query string of the form action url) Once the file upload has started, fire Ajax request to `/progress?X-Progress-ID=<GUID>` to get the status of the upload.
- The status would be in a Json format.
Ex -
{% highlight js %}
{ "state" : "uploading", "received" : 35587, "size" : 716595, "speed" : 35587, "started_at": 1296568823, "uuid" : "12345678" }
{% endhighlight %}

#### Fields -

  - state - indicates the current status of the upload. Once the upload is complete, the state would be 'done'

  - received - indicates the number of bytes received by the server.

  - size - total size of the file in bytes

  - started_at - upload start time. (Epoch format)

  - uuid - The GUID supplied as part of the query string key (X-Progress-ID)

## Reference -

[README of apache-upload-progress-module](https://github.com/drogus/apache-upload-progress-module)
