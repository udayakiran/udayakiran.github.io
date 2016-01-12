---
layout: post
title: "Browsers - Chrome dropped support for NPAPI plugins. What's next?"
description: "Browsers - Chrome dropped support for a number of plugins. What's the reason? What's next?"
tags: [java, browsers, web, Java web start, HTML5]
image:
  feature: abstract-6.jpg
  color: "1abc9c"
  icon: "clock-o"
bg_color: "1abc9c"
---

Starting September 1, 2015, Google chrome dropped the support for NPAPI plugins. So, Chrome 45+ versions do not support a number of plugins which depend on this. This is not a sudden change and is expected for some time now. This means a number of java, silverlight, Unity and Facebook plugins do not work any more on Chrome. Well, this is not a surprise unless you are not following chrome's regular updates on this topic.

* Chrome expressed their wish to block this way back in September, 2013. (Ref - <http://blog.chromium.org/2013/09/saying-goodbye-to-our-old-friend-npapi.html>)

*  Chrome web store stopped accepting any new NPAPI based apps since September, 2013.

* In November, 2014 this is confirmed and deprication timeline is announced (Ref - <https://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html>)

* As said, Chrome 42 (released in April, 2015) disabled these plugins by default with a hack to enable this support as an experimental feature.

* Google started to move their Gtalk's architecture completely to hangouts and made themselves ready for the big move. The time announced was sufficient enough for many apps to prepare themselves for the change.

* Finally, Chrome 45 (released in September, 2015) stopped the support for NPAPI plugins.

## Why was the support dropped ?

Chrome quotes on it's web site that -

> To make browsing with Chrome safer, faster, and more stable, we stopped allowing NPAPI plugins on September 1, 2015.

 (Ref - <https://support.google.com/chrome/answer/6213033?hl=en>)

* We can clearly see that there is intention to improve the speed of the browser by making sure that plugins and apps are run independent of the browser once launched. (This wasn't the case with NPAPI).
* Also, we can see that this step of chrome is a push forward through more HTML5 based apps (WebRTC and etc.), browser extensions and one click install cross device apps.
* This is going to be a major hit for traditional plugin apps like java applets and silverlight apps.

## What's next for the apps that depend on NPAPI ?

Both Java and silverlight responded by providing a workaround to run the plugin based apps for Chrome 42 to 44. But from Chrome 45, it's not possible any more. So, they recommend to use a browser which supports NPAPI plugins. Java recommends to use Web Start apps which are like one click install apps, that does not depend on browser once installed and launched. Chrome too, suggested various alternatives to handle stuff in future.

- From Java - <https://java.com/en/download/faq/chrome.xml>
- From silverlight - <https://support.microsoft.com/en-us/kb/3058254>
- From Chrome - <https://www.chromium.org/developers/npapi-deprecation>


It's clear that chrome's push is towards WebRTC for the media and WebGL for gaming and animation. However, i am going to focus a bit on the java web start apps below which is one nice way to have cross browser and cross device one click install based apps that need to be launched from browsers. For one of my personal projects i went ahead to convert a java applet to JNLP based web start app which worked well.


### Java Web Start apps -

Java Web start technology is shipped with your JDK and all that the user need to have is java installed on their local machines to run the apps based on this.

* **Introduction to Web start apps -**
  [Java Web Start Intro](https://www.java.com/en/download/faq/java_webstart.xml)

* **Running a Web start app -**
  [Running Web Start apps](https://docs.oracle.com/javase/tutorial/deployment/webstart/running.html)

* **Migrating Java applets to JNLP Web start apps -**

  [Applet Migration Guide](https://docs.oracle.com/javase/7/docs/technotes/guides/jweb/applet_migration.html)

  [Applet Dev Guide](http://docs.oracle.com/javase/8/docs/technotes/guides/deploy/applet_dev_guide.html#CIADJHDC)

* **Simple tutorials -**
[Web start and JNLP Tutotial 1](http://www.mkyong.com/java/java-web-start-jnlp-tutorial-unofficial-guide)

[Web start and JNLP Tutotial 2](http://media.techtarget.com/searchDomino/downloads/CH14_0672326280.pdf)

* **JNLP app demos -**
  [JNLP Demos](http://docs.oracle.com/javase/tutorial/uiswing/examples/misc/index.html)

* **Web start appp demos -**
  [Web Start Demos](http://goworldwind.org/demos/)


> Web start apps are good for now but looking forward, it is most likely that WebRTC and other HTML5 improvements can replace all the plugins and it's just the matter of time before Safari starts supporting WebRTC.
