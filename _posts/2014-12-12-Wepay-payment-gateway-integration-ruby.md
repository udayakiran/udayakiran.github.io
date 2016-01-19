---
layout: post
title: "Ruby/Rails - Wepay payment gateway integration"
description: "Integrating a rails app with wepay's APIs"
tags: [ror, ruby, web]
image:
  feature: abstract-6.jpg
  color: "009688"
  icon: "clock-o"
bg_color: "009688"
---

Since it's launch, wepay has been a great payment gateway which provides best user experience along with developer friendly integration. I use this for a number of web and mobile apps and feel that this is one of the best way to handle one time purchases, recurring payments and etc. without having to store any details of the customer's credit card.

I am going to share a few ideas on how to integrate wepay with your rails/sinatra app.

## Getting Started -

Wepay has an excellent developer's site which has every single detail you may expect as a beginner. Their support is very responding and helpful. Will mention some of the important links below so you can get some help and start.

1. Developers site - <https://www.wepay.com/developer>
2. API documentation - <https://www.wepay.com/developer/reference>
3. SDKs - <https://www.wepay.com/developer/resources/sdks>
4. Some use cases -
    - <https://www.wepay.com/developer/usecases/tipping-point-payments>
    - <https://www.wepay.com/developer/usecases/delayed-payouts>
    - <https://www.wepay.com/developer/usecases/subscription-payments>
    - <https://www.wepay.com/developer/usecases/mobile-app>

Find some implementation specific details below.

## Implementation with ruby -

We can use wepay's ruby SDK to integrate your rails/sinatra app with wepay. But i m going to do this by using one of the gems we developed for ourselves. Either should do fine.

Source - <https://github.com/udayakiran/wepay_client>

Please refer README for details on how to use this.

## Setup and usage

### Setup

In rails put following in Gemfile


{% highlight ruby %}

gem 'wepay_client',:git => 'git://github.com/udayakiran/wepay_client.git'

{% endhighlight %}

### Usage

Create a wepay_config.rb in config/initializers folder and setup the client with wepay client id and client secret

{% highlight ruby %}

require 'wepay_client'

WepayClient::Client.configure do
  client_id     '11111111'
  client_secret '5f434343'
  use_ssl       true
  use_stage     !(ENV['RAILS_ENV'] == 'production')
end

{% endhighlight %}

An example to call wepay apis

{% highlight ruby %}

wepay = WepayClient::Client.instance
account = wepay.create_account('token data', 1122334)
p account[:account_id]

{% endhighlight %}

## Alternates -

As mentioned above, Wepay provides a ruby SDK for the same purpose - <https://github.com/wepay/ruby-sdk>

wepay's SDK can be used if you find it more comfortable. We started this wepay_client gem during the initial days when there was no ruby SDK from wepay. There are a few differences in the design and i think we are doing a little better job of handling exceptions and converting response to proper ruby objects.

However, both of these sever the same purpose. So, either can be chosen without a thought. We try our best to keep this gem up to date and well maintained.
