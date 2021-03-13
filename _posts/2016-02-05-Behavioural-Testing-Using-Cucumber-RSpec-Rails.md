---
layout: post
title: "Behavioural Testing Ruby/Rails Apps @ Scale with Rspec and Cucumber"
description: "Behaviour Testing "
tags: [javascript, web, js library, ror]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

## Problem -

When I used to lead the development of a functional heavy e-learning cloud (it's like Shopify for e-learning) we used to have a fairly large code base written in Ruby (Rails) and nodejs. To understand the scale, there were 250+ APIs used by hundreds of websites launched on this cloud platform. 

<div style="text-align: center">
<figure class="full">
	<img src="/images/rails-rspec.png" width="600px" alt="">
</figure>
</div>

We had a development team of size 40+ spread across 3 engineering centers and integration testing used to be an issue. This demanded a lot of cross team coordination efforts to perform releases on a daily cadance and resulted in slower deployment cycles. The platform was under development for 3+ years already and had good unit and functional test coverage.  I decided to lead an effort towards increasing our integration test coverage, automate behavior testing so that SDE bandwidth is saved during integration and UAT is fast tracked by QA being able to run all behavior tests in self service manner.

## Solution -



<div style="text-align: center"><iframe src="//www.slideshare.net/slideshow/embed_code/key/k5jytoDvnMLyyA" width="695" height="585" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/secret/k5jytoDvnMLyyA" title=" Behavioural Testing Ruby/Rails Apps @ Scale - Rspec &amp; Cucumber" target="_blank"> Behavioural Testing Ruby/Rails Apps @ Scale - Rspec &amp; Cucumber</a> </strong> from <strong><a href="https://www.slideshare.net/udayslideshare" target="_blank">Udaya Kiran</a></strong> </div></div>

## Results

1. This saved a cumulative of 1.5 SDE and 2 QA bandwith for releases through out the month.
2. Test coverage for code improved from 65% to 87%
3. Number of regression bugs reduced by 10% upon release.