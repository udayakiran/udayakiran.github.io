---
layout: post
title: "JavaScript - Templating with embedded js (no more ugly HTML inside js)"
description: ""
tags: [javascript, web]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---

## Why ? -

[Embedded js](http://www.embeddedjs.com/) is a client side templating library, which is used to write cleaner HTML and JS code in the places that render html dynamically with javascript. Results in easy to write, clean, readable and maintainable code base.

## Problem -

We have been working on a simple ajax based messaging app where as messages come they are updated in the UI through ajax. The messages are of different types and each type has a different html layout structure we need to construct based on the ajax's response. This caused some parts in the code that look like below -

{% highlight text %}

  var text_messages = function(data) {
    var html = "<h1>"+data.title+"</h1>"
  html += "<ul>"
  for(var i=0; i<data.supplies.length; i++) {
      html += "<li><a href='supplies/"+data.supplies[i]+"'>"
      html += data.supplies[i]+"</a></li>"
  }
  html += "</ul>"
	$('calendar_content').innerHTML = html;
}

{% endhighlight %}



## Solution -
