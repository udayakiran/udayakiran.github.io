---
layout: post
title: "Ruby/Rails - Ajaxifying a rails app with ajaxify-rails gem"
description: "Ajaxifying a rails app with ajaxify-rails
gem and a few other tweaks."
tags: [ror, ruby, web]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

Below are some of the details on how to convert a traditional synchronous rails webapp to a complete ajax app. Will try to list out a the gems used for this and lessons learnt during this process.

<div style="text-align: center">
<figure class="full">
	<img src="/images/ar.png" width="600px" alt="">
</figure>
</div>

### Why do you need this ?

The main reason we wanted to do this is to keep the user on the same page through out the interactions. This was needed as we were supporting webRTC based voice calls through websocket connections, which we did not want to drop when user navigates across the pages.

### Requirements -
We wanted to convert a rails 4.2 app to completely ajax. Followig are some of the requirements.

- App should work like a single page app without any new page navigation.
- Code changes need to be as minimum as possible.
- There should be a clear feedback to the users while ajax requests are in progress.
- We should be able to support page specific assets (js, CSS and images)
- Assets and specific sections of the page need to be reloaded after deployments.

# Implementation -

Following gems are used with a few tricks to achieve all our requirements.

[Ajaxify-rails](https://github.com/udayakiran/ajaxify_rails) - ajaxifying the app (works similar to turbo links). This is a clone of [ncri's repo](https://github.com/ncri/ajaxify_rails) with a few bug fixes and one enhancement.

[Gon](https://github.com/gazay/gon) - Pass ruby variables to javascript (typically from controllers)

[Pace](http://github.hubspot.com/pace/) - Youtube style horizontal progress bar.

## Basic ajaxification implementation -

ajaxify_rails gem is preferred for this over turbo_links for one major reason i.e As of rails 4.2 turbo links gem always replaces the body tag. We cant specify different containers which need to be updated for different ajax requests. There is a mention that this will be solved in rails 5 and future versions of turbo links. So, ajaxify_rails worked very well for us here.

Following are the details of ajaxify_rails gem and how certain things are handled during ajaxification.

### About the gem -

#### Features -

- Automatically turning internal links into ajax links that load content without a full page reload.
- Form submissions are converted to ajax as well.
- Provides a way to specify the 'content_container' which needs to get the ajax response updated.
- A number of callbacks are available to perform things during ajax life cycle.

#### Improvements neeeded -

- One thing that this gem lacked in it is to reload the whole page after deployments if a specific view file or layout file has changed. But we could add this ourselves and the code is present in [My git repo](https://github.com/udayakiran/ajaxify_rails).

#### Usage -
- Ajaxify.init() is called on `dom:loaded`
- By default the response of the ajax request is updated inside a element with id “main”. This can be changed for each ajax request by setting “content_container” value as needed.

#### Few internals -
- Page title is supported by default.
- Loader can be customized with our own css to the element “ajaxify_loader”
- Loader can be disabled by setting “display_loader” to false while initializing or by setting class “display_loader” or “no_display_loader” to each link we are ajaxifying.
- Flash messages are supported by default. If flash message of types other than “notice” is used then it should be specified as “flash_types” while initializing.

#### Events & Callbacks -

There are a number of events supported e.g - content_loaded, flast_displayed, before_load, content_inserted, load_error and etc. JS callbacks can be written for each of these events.

#### Scrolling -

By default the page scrolls to to the top on every request. This can be turned off by setting “scroll_to_top” to false while initializing. Scrolling of individual links can also be turned off or turned on by setting class “no_scroll_to_top” or “scroll_to_top”

#### Turn off ajaxification -
Ajaxification can be temporarily turned off for some pages using Ajaxify.activate(false) and can be turned on using Ajaxify.activate().

#### Loading controller specific assets -

Normal requests are served through one layout where as ajaxified requests are served with a layout which has the normal layout wrapped in. We include the contoller specific assets in this layout.

#### Expiring assets after deployment -

ajaxify_rails gem provides a way to expire the assets (js, css and images) after deployment. It reloads the whole page with the first ajaxified request after the deployment. The only change needed for this to work is to make sure the below option to true in your envionment file (staging.rb/development.rb/production.rb)

{% highlight ruby %}

Rails.application.config.assets.digest = true

{% endhighlight %}

#### Reloading the whole page when any layouts/app logic changes -

Say you have made the changes to some view files and after the server restart, the already opened pages are required to reload whole page instead with ajax, there is a way provided for this. You ll have to just assign array of those filenames along with some digest.

{% highlight ruby %}

Rails.application.config.layout_digests = ['xyz.haml-efegegegega787878']

{% endhighlight %}

To create this list, following code can be added in an initializer file.

{% highlight ruby %}

FILES_TO_BE_OBSERVED = ["app/views/layouts/_header.html.haml","app/views/layouts/_logo.html.haml"]  
digests = []
FILES_TO_BE_OBSERVED.each do |filename|
  begin
    digests << Digest::SHA256.file(filename).hexdigest
  rescue
    next
  end
end

Rails.application.config.layout_digests = Digest::MD5.hexdigest(digests.join)

{% endhighlight %}

## Passing ruby variables to JS -

We had a specific case where we wanted to update a particular div out side the content div after every ajax response. The value of the div comes from controller with every request. So, this needed us to have a way to pass the controller variables to javascript.

This was done by using [Gon gem](https://github.com/gazay/gon)

- Gon passes the controller variables to javascript assets files as js variables.
- Gon has to be initialized for every request, by including “include_gon(:init => true)” in the layout file.
- Any controller variable is declared as “gon.variable_name = something” in the controller and can be accessed in the javascript by “gon.variable_name”

## Youtube style progress bar with pace -

We wanted to give a clear feedback about the progress of the ajaxified requests. One good UX for this is to show a progress bar at the top of the page like how You tube and many other apps do.

This was done using [Pace](http://github.hubspot.com/pace)

- By default pace gem displays the progress bar for page load requests, ajax requests, ajaxified requests as well as for the elements which we can specify (default element is body tag).

### Apis provdided by Pace -

 start, restart, stop, track and ignore.

### Events and callbacks -

start, restart, stop, done, hide.

### Usage -

Include pace.js and set the options for page using “window.paceOptions = {}”

For more details refer the [Hom page](http://github.hubspot.com/pace)


>> Ajaxification of an already built app was really cool and glad that we could do it with minimal code change in a clean way. This helped us in improving the speed of the app and also helping to stay on a single page and do a lot of things, there by persisting the websocket connections and etc. while navigating in between different page links.
