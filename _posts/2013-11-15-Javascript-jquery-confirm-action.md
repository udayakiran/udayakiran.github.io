---
layout: post
title: "JavaScript - jQuery.confirmAction.js (Minimalistic jquery plugin to confirm actions in a pretty way)"
description: "JavaScript library - jQuery.confirmAction.js: Confirm users actions in a pretty way without having to use browser confirm box / alert box."
tags: [javascript, programming, web, js library, jquery plugin]
image:
  feature: abstract-6.jpg
  color: "009688"
  icon: "clock-o"
bg_color: "009688"
---

## Why ?

This is a jQuery plugin that confirms an action on click of an element and executes separate js code based on the confirmation.

Can be used to confirm users actions in a pretty way without having to use browser confirm box / alert box.

## Info -

* Source code - <https://github.com/udayakiran/jQuery.confirmAction.js>

## Setup & Usage -

1. Download jquery.confirmAction.js OR jquery.confirmAction.min.js

2. Include jQuery file (1.7+) and the plugin file (or .min file) in your HTML page.

{% highlight html %}

<script type="text/javascript" src="https://code.jquery.com/jquery-1.7.1.min.js"></script>
<script src="jquery.confirmAction.min.js"></script>

{% endhighlight %}

#### Example usage -

Say there is a link/button with id "confirm_link", if you want to display a confirmation message to the user on clicking this link and decide weather to proceed or not -

{% highlight html %}

<script type="text/javascript">

     jQuery(document).ready(function () {
        jQuery("#confirm_link").confirmAction({container: jQuery("#<container_id>"),
          text: "<Text that describes the confirmation related info>",
          confirmButton: "<Confirm button label>",
          cancelButton: "<Cancel button label>",
          avoid_confirm_double_click: true,
          cancel: function() {
            //Code to be executed on clicking cancel button.
          },
          confirm: function() {
            //Code to be executed on clicking confirm button.
          }
        });
      });    

 </script>
 
{% endhighlight %}
