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

  var html = "<h1>"+Messages since" + data.last_seen.toString() +"</h1>";
  html += "<ul>";
  for(var i=0; i<data.messages.length; i++) {
      html += "<li><a href='profiles/"+data.messages[i].senderID+"'>"</a>";
      html += "<span class='msg-content'>" + data.messages[i].text + " </span>";
      html += "<span clas='msg-date'>" + data.messages[i].receivedAt + "</span>";
      html += "</li>"
  }
  html += "</ul>"
  $('more_message_content').innerHTML = html;
}

{% endhighlight %}

It can be observed from the above code that both HTML and js mixed in a way that it is not easy to read and debug. This is a simpler example compared to our code base and a lots of other complex JS heavy apps.


## Solution with Ejs templates -

Embedded JS lets us write the js code inside html look a like template structure. Templates can be maintained as separate files to which data can be passed.

This results in a code base that looks like this -

{% highlight text %}

  <h1>'Messages since <%= data.last_seen.toString(); %> </h1>
    <ul>
      <% for(var i=0; i<data.messages.length; i++) { %>
          <li>
              <a href='profiles/<%= data.messages[i].senderID%>'></a>
              <span class='msg-content'> <%= data.messages[i].text %></span>
              <span clas='msg-date'><%= data.messages[i].receivedAt %></span>
          </li>
      <% } %>
    </ul>

{% endhighlight %}

Lets call the above template as messages.ejs and it can be rendered like

{% highlight text %}

var callback = new EJS({url: 'templates/calendar.ejs'}).update('more_message_content');

{% endhighlight %}

We can clearly see that this code, after cleanup looks like HTML - more readable and maintainable.

## Other benefits of Ejs -

 - Supports number of view helpers.

 - Supports partials which means templates can be embedded in other templates making them reusable.

 - Support caching of the templates.

## Ejs References -

  - Homepage - http://www.embeddedjs.com/

  - GettingStarted - [Gettng Started](http://www.embeddedjs.com/getting_started.html)

  - Screencast - <http://www.embeddedjs.com/screencast/index.html>


>> If you still are writing your ajax html code inside your JS, it's the time to clean it up with embedded js.
