---
layout: post
title: "Leadership - Learnings from Large Scale Migrations"
description: "Large scale system migrations have lots of impact on organizations, people and culture. Cost is too high some times."
tags: [java, browsers, web, Java web start, HTML5]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---


> Yahoo! Search (Desktop) 2.0
>
> *Reimagined for better Ad revenue*
>
> *We are proposing 3 buckets of suggestions to optimize Yahoo! Desktop Search for better Ad revenues. Over the long run, this is expected to uptick the ad revenues by X%. This uptick is a result of A% increase in CTR, B% of new ad placements and C% of additional traffic.*
>
> **(A) Get Fitter: UX changes to improve CTR with existing ad placements [Low investment]**
>
> 1. Search listing UX.
> 1. Brand Favicons + Ad labels.
> 1. Selective Attention experiments.
>
> **(B) Get Better: Modify/Introduce new ad placements + improved UX from (A) [Medium investment]**
>
> 1. Better in-page ad placements
> 1. Efficient use of real-estate.
> 1. More Product Listing ads on search results
>
> **(C) Get Big: Reinvent and go big [High investment]**
>
> 1. Feed based UI for search results
> 1. Anticipatory/Predictive ads
> 1. Push mechanisms for search results.
>
> **Background:**
>
> 1. Users scan through search results. It’s either a linear top to bottom scan (for simple search pages) or random hotspot check (for pages with images and other interactive blocks). 
>
> 1. Rarely users go to page 2 (<X%).
> 1. Users are automatically trained to ignore the information they do not want to look at (Ex - URL links of search results, default ad placements and ad labels).
> 1. With mobile generation, a scroll is considered a casual effort and a click/touch is a costly effort during browsing.
>
> **(A) Get Fitter: Improve CTR with existing ad placements**
>
> 1. **Search listing UX:**
>
> To be updated with changes like fonts, placement of links, Title and other details.
>
> **Sample UI:**
>
> **Pros:**
>
> **Cons:**
>
> 1. **Brand Favicons + Ad labels:**
>
> Show favicons of each of the websites beside the link text of each search result. For ads use a black/gray “Ad” label.
>
> **Sample UI:**
>
> 
>
>
> Fig: Comparison - with vs without favicons
>
> **Pros:**
>
> 1. Users get automatically trained to look for favicons and improve the traction on ads. “Ad” tag can be experimented with options to avoid “banner blindness”.
> 1. Such favicons improve CTR for both organic search results and ads.
> 1. Brand awareness improves for publishers.
> 1. Ads look more native within the content. 
> 1. Already proven on mobiles. Works well across platforms.
>
> **Cons**:
>
> 1. There could be some publishers/websites without favicons. Or, they may not want the same icon across all their content. This may require a new search meta data tag that needs to be provided, in which case, the crawlers need to be upgraded to identify this.
>
> **Measure of Success:**
>
> - CTR for organic search results
> - CTR for ads
> - Time spent by users on search results.
> - Brand value improvement
>
> 1. **Selective Attention experiments:**
>
> Run experiments with various options to ensure users are countered from “banner blindness”. Examples:- change the Ad format, labels, backgrounds etc.
>
> Fig: Yellow background for Ads
>
>
> Fig: Experiments with and without favicons. Also, change in ads label style
>
> **Pros:** 
>
> 1. Counters users’ “banner blindness”.
> 1. Better user experience and lets you figure out things iteratively.
>
> **Cons:**
>
> 1. Frequent changes might lead to user surprise. 
>
> **Measure of Success:**
>
> - CTR for organic search results
> - CTR for ads
>
> **(B) Get Better: Modify/Introduce ad placements + improve CTR**
>
> **1. Better in-page ad placements:**
>
> As mentioned above, users either scan linearly or look for random spots in the ads. Some of the common hotspots are highlighted below. Place your ads below these hotspots. Choose right ad type near the hotspots (Ex - Product listing type ads at the top, text beneath images etc.). As of now Yahoo search seems to have ads only in the top and bottom of search results listing.
>
> 
>
> 
>
> 
>
>
> **Pros**:
>
> 1. More ad placements and more traction of the users.
>
> **Cons**: 
>
> 1. Experience might get mixed responses from users unless carefully designed.
>
> **Measure of Success:**
>
> - Increase in number of impressions.
> - Increase in CTR.
>
> 1. **Efficient use of real-estate.**
>
> Some of the sections such as the top of the page and “right side column” of the entire search page are not used to good extent. If carefully designed, they can work as powerful ad placements.
>
> **A few examples:** Keep the right hand side ads sticky while user scrolls, refresh the ads every time user scrolls again. Choose native and product listing ads here.
>
> As of now “car cleaning” does not show any ads. There is a good chance to use the right hand panel here to show product listing type ads.
>
> 
>
> **Pros:**
>
> ` `To be updated
>
> **Cons:**
>
> `  `To be updated
>
> **Measure of Success:**
>
> - Increased placeholders for ads
> - Increased impressions
> - Increased CTR.
>
> 1. **More Product Listing ads on search results:**
>
> Focus more on product listing style ads in search results. They can be app installs, registrations or e commerce related ads.
>
>
> **(C) Get Big: (Reinvent and aim big with ads)**
>
> 1. **Feed based UI for search results:**
>
> Scroll is always a less costly interaction than a click due to modern hardware. Hence pagination on desktop and mobile search can be replaced with feed style UI. This also solves the problem of users not visiting page 2 much. This can be experimented on mobiles first and then on desktop. Gives chance to introduce many native ads if implemented successfully.
>
> 
>
> 
>
> 1. **Anticipatory/Predictive ads:** 
>
> While a user types “hair dryer” no ads are shown but when he types “best hair dryer” ads are shown. Search has “also try” functionality which can be applied to ad keywords. Think ahed of “also try results” and show ads for those as well in the current page. Ex: When user types “hair dryer” also show ads for “best hair dryer” that makes sense.
>
> 1. **Push mechanisms:** Find push methods to deliver search data to user and use it as channel for ads. Similar to Google feed, keep pushing search/news/trending results stream as per user's interest. This can act as a potential ad channel.
>
> **Internal References -** 
>
> <https://www.youtube.com/watch?v=DfEIpj1ewPw>
>
> <https://uxdesign.cc/why-googles-new-search-results-design-is-a-dark-pattern-168935802f95>
>
> <https://moz.com/blog/is-googles-redesign-good-for-ads-or-brands>
>
> <https://www.theverge.com/2020/1/24/21080424/google-search-result-ads-desktop-favicon-redesign-backtrack-controversial-experiment>
>
> <https://www.blog.google/products/search/feed-your-need-know/>
