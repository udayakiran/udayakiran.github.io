---
layout: post
title: "Desktop Web Search Engine Results Page - Design Considerations for Better Ad Revenues"
description: "Research summary of a search engine results page design and recommendations for better Ad yields."
tags: [Ads, UX, Design, web, product]
image:
  feature: abstract-6.jpg
  color: "616161"
  icon: "clock-o"
bg_color: "616161"
---

Search is our gateway to internet and advertisements/sponsered content are the backbone of search engines. In this post, I am propsing a few UX design suggesstions to the deskop search engine results pages to improve the ad revenues. These are based on analysis and benchmarking current search engine landscape. .

<div style="text-align: center">
<figure class="full">
	<img src="/images/SERP-Features.jpg" width="600px" alt="">
</figure>
</div>

I have bucketized the suggestions into 3 groups based on amount of investment to implement these changes. Over the long run, this is expected to uptick the ad revenues by X%. This uptick is a result of A% increase in CTR, B% of new ad placements and C% of additional traffic

- **A) Get Fitter: UX changes to improve CTR with existing ad placements [Low investment]**
- **B) Get Better: Modify/Introduce new ad placements + improved UX from (A) [Medium investment]**
- **C) Get Big: Reinvent and go big [High investment]**

#### Below are a few Initiatives proposed across these buckets:


| Get Fitter | Get Better | Get Big |
|:--------|:-------:|--------:|
| Search listing UX.   | Better in-page ad placements   |  Feed based UI for search results   |
| Brand Favicons + Ad labels.  | Efficient use of real-estate.   | Anticipatory/Predictive ads   |
| Selective Attention experiments.   | More Product Listing ads on search results   | Async delivery for search results.   |
{: rules="groups"}

----



## **User Behavior Background:**

1. Users scan through search results. It’s either a linear top to bottom scan (for simple search pages) or random hotspot check (for pages with images and other interactive blocks). 

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="/images/lin-scan.png" width="400px" alt="">
  	<figcaption style="text-align: center"> Linear Scan through page</figcaption>
  </figure>
</div>

<div style="text-align: center">
<figure class="">
	<img src="/images/pinball.png" width="400px" alt="">
  	<figcaption style="text-align: center"> Random/Pin ball style Scan through page</figcaption>
  </figure>
</div>

2. It'a rare that users go to page 2 (< X%).

3. Users are automatically trained to ignore the information they do not want to look at (Ex - URL links of search results, default ad placements and ad labels).

4. With mobile generation, a scroll is considered a casual effort and a click/touch is a costly effort during browsing.

## **(A) Get Fitter: Improve CTR with existing ad placements**



1. ### **Brand Favicons + Ad labels:**

Show favicons of each of the websites beside the link text of each search result. For ads use a black/gray “Ad” label.

#### **Sample UI:**

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh4.googleusercontent.com/7Jo4nbCLg-nvslSqMv-pd5L-0DsBg5U1CoxV3PXKTRJ4hDJ6-2JNZ0kI9EPPz6xNmQkZHVmcF53B5BkwBySXS3MsB7rQKMuYjilxzhW4PAiXj90yPpZM3q3097oNfyZPMTjHTk_u" width="600px" alt="">
  	<figcaption style="text-align: center"> Results with favicons</figcaption>
  </figure>
</div>

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh3.googleusercontent.com/W8BdFDTKmndZrBg0gkbHW4VEtjI8-1y5RH-KEqDsT9zUEu2ZwoLvSKizZQ7PC2cKMzDRsKsZ1qdk8vQxV7ydnMFT2ebMCaVY9vCSKSnbAM7Mx9oQp0kyKtFzE8N69neiHnwiIg88" width="600px" alt="">
  	<figcaption style="text-align: center"> Results with favicons - Highlighted</figcaption>
  </figure>
</div>

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="/images/with_without_favicons.png" width="800px" alt="">
  	<figcaption style="text-align: center"> Fig: Comparison - with vs without favicons
</figcaption>
  </figure>
</div>

**Pros:**

1. Users get automatically trained to look for favicons and improve the traction on ads. “Ad” tag can be experimented with options to avoid “banner blindness”.
2. Such favicons improve CTR for both organic search results and ads.
3. Brand awareness improves for publishers.
4. Ads look more native within the content. 
5. Already proven on mobiles. Works well across platforms.

**Cons**:

1. There could be some publishers/websites without favicons. Or, they may not want the same icon across all their content. This may require a new search meta data tag that needs to be provided, in which case, the crawlers need to be upgraded to identify this.

**Measure of Success:**

- CTR for organic search results
- CTR for ads
- Time spent by users on search results.
- Brand value improvement

1. **Selective Attention experiments:**

Run experiments with various options to ensure users are countered from “banner blindness”. Examples:- change the Ad format, labels, backgrounds etc.



<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh5.googleusercontent.com/IhIcR280J72NKduu120z_7z5cK-yTMVJFMxslLNAQTfpFJg2GxEDm7c5EdBnfdXGJRDZr7t-0TBO36x8OJdZabbRQLupcu_AIBCQ9DIaLQEJR-GD0UYIsofGwEtaf6soFf5NiCmc" width="600px" alt="">
  	<figcaption style="text-align: center"> Fig: Yellow background for Ads
</figcaption>
  </figure>
</div>

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="/images/ad_labels_favicons.png" width="800px" alt="">
  	<figcaption style="text-align: center"> Fig: Change in favicons lable styles.
</figcaption>
  </figure>
</div>

**Pros:** 

1. Counters users’ “banner blindness”.
2. Better user experience and lets you figure out things iteratively.

**Cons:**

1. Frequent changes might lead to user surprise. 

**Measure of Success:**

- CTR for organic search results
- CTR for ads

### **(B) Get Better: Modify/Introduce ad placements + improve CTR**

#### **1. Better in-page ad placements:**

As mentioned above, users either scan linearly or look for random spots in the ads. Some of the common hotspots are highlighted below. Place your ads below these hotspots. Choose right ad type near the hotspots (Ex - Product listing type ads at the top, text beneath images etc.). As of now Yahoo search seems to have ads only in the top and bottom of search results listing.

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh5.googleusercontent.com/IZz-PBZwENy43ZNA7MKPHvrB3eG3hFUDlNrFom0x6r0V5v4ieCAnttFAKL7knDMF8bRe2NmScS5_EW4EyQpyCRhCJP13G9OqLaanxDisseSCJRssPXWtBsJe6NoLITVF2xG_5E53" width="800px" alt="">
  	<figcaption style="text-align: center"> Fig: Ad placements considering pin ball scanning behavior.
</figcaption>
  </figure>
</div>



<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh6.googleusercontent.com/RY5fw3iaMgGp3v1vAk1X-hq9hnjEDMH7viCarWUdk9lZoTSk24o3ymBlNXvDEZhFwUiqkZkprxLbmYK0x0A-M6-lZK1XpP-X1E_f4LwDdOn2JmWsmCO2XdvFOr_iYQduUgJTuYQS" width="800px" alt="">
  	<figcaption style="text-align: center"> Fig: More ad placements following scroll based pagination.
</figcaption>
  </figure>
</div>

**Pros**:

1. More ad placements and more traction of the users.

**Cons**: 

1. Experience might get mixed responses from users unless carefully designed.

**Measure of Success:**

- Increase in number of impressions.
- Increase in CTR.

2. #### **Efficient use of real-estate.**

Some of the sections such as the top of the page and “right side column” of the entire search page are not used to good extent. If carefully designed, they can work as powerful ad placements.

**A few examples:** Keep the right hand side ads sticky while user scrolls, refresh the ads every time user scrolls again. Choose native and product listing ads here.

As of now “car cleaning” does not show any ads. There is a good chance to use the right hand panel here to show product listing type ads.

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh6.googleusercontent.com/Caw-VNWHd7n-3tCRE21GBJyYXsKn5R--eZ0t2zEOUeMKPLj_zIAAJ6uaVAxAd5Td1rzrJ3dfjm12dA8nuKR3-_-ss5aCro9Hza7s8eD5P8CHq45rgsXu5ofmHUu0RTHYuYc0OQ6-" width="800px" alt="">
  	<figcaption style="text-align: center"> Fig: Use right half of screen for ad placements.
</figcaption>
  </figure>
</div>

**Pros:**

` `More ads resulting more revenue.

**Cons:**

Can get cluttered unless desinged well leading to loss of focus on search results.

**Measure of Success:**

- Increased placeholders for ads
- Increased impressions
- Increased CTR.

#### **2. More Product Listing ads on search results:**

Focus more on product listing style ads in search results. They can be app installs, registrations or e commerce related ads.

### **(C) Get Big: (Reinvent and aim big with ads)**

#### 1. **Feed based UI for search results:**

Scroll is always a less costly interaction than a click due to modern hardware. Hence pagination on desktop and mobile search can be replaced with feed style UI. This also solves the problem of users not visiting page 2 much. This can be experimented on mobiles first and then on desktop. Gives chance to introduce many native ads if implemented successfully.

<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh6.googleusercontent.com/RqUPmROrSic8pk75tcbsRhJYnk-7U_B479jbcdd0v-cwvgadqrjdha1BX6qARYwpxUAlDCG3-CkwHDbBr-Ef0I0xaOn238PzR-6l9sYORWI2oLjcne6dmknCx85QLqDqFqI6aH0o" width="400px" alt="">
  	<figcaption style="text-align: center"> Fig: Feed based UI with sponsered content
</figcaption>
  </figure>
</div>



<div style="text-align: center; display:inline;">
<figure class="">
	<img src="https://lh4.googleusercontent.com/M6ccnMSLL94yeHDlZf3vaHlne650xeSzaHtfxo_T8byjXKe2v34yYVtVhCeX6A7kOCDdoCdYDBdJ4tUPknh716e8ZD3o-2pw4QRS3haPWPmEI9NZ3sh954VYnLQ2qk8ji9zhvCgh" width="600px" alt="">
  	<figcaption style="text-align: center"> Fig 2: Feed based UI with sponsered content
</figcaption>
  </figure>
</div>

#### 2. **Anticipatory/Predictive ads:** 

While a user types “hair dryer” no ads are shown but when he types “best hair dryer” ads are shown. Search has “also try” functionality which can be applied to ad keywords. Think ahed of “also try results” and show ads for those as well in the current page. Ex: When user types “hair dryer” also show ads for “best hair dryer” that makes sense.

#### 3.**Async results devilry (Push results offline):**** 

Find methods to deliver search data to user and use it as channel for ads. Similar to Google feed, keep pushing search/news/trending results stream as per user's interest. This can act as a potential ad channel.