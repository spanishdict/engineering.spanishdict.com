---
layout: post
author: Chris Cummings
author_link: http://www.spanishdict.com/company/people
title: Front End Profiling and Optimization
description: Learn about how SpanishDict set out to profile
  and optimize its frontend code. 
date: 2012-03-12 18:01:00 UTC
tags: ['frontend', 'performance', 'profiling', 'optimization']
---

{% capture img_dir %}{{ site.baseurl }}media/img/{{page.date|date: "%Y/%m/%d"}}{% endcapture %}

[![Go Front End Go!][speed_racer_img]][speedracer]

[speed_racer_img]: {{ img_dir }}/go_speed_racer_go.jpg

The benefits of a fast load times are [well][shopzilla] 
[documented][kissmetrics]. But increasingly, loadtime is about more than just 
the application and database. The front-end is now critical, so much so it 
[influences][webmastertools] search rankings. 

Our application loads a page, on average, in under 50ms. Network time can add 
another 100-200ms (see 
[Google Pagespeed][pagespeed], 
[Yahoo YSlow][yslow], and 
[WebPageTest][webpagetest] for ideas on how to improve this 
area). But the total time before a user can see our content had climbed to 
upwards of 500ms. The culprit? Well, we had to setup some profiling tools 
to find out.

Front-end profiling can be something of a dark art. We used:

* [Google Chrome Developer Tools][chromedev]
* [Firefox and Firebug][firebug]
* [DynaTrace's Ajax 3][dynatrace]

But perhaps the most essential tool was a good old fashion console timer that 
we could insert at various parts of the code. 

### Setting up Profiling

We tied our benchmarks to the DOMContentLoaded event, which marks when 
parsing of the document has finished. To measure performance across browsers, 
we used a [cross-browser method][crossbrowser] to capture the DOMContentLoaded 
event. We also patched older versions of IE with a 
[console.time function][console]. Here is roughly how the code looked:

{% highlight html %}
<html>
  <head>
    <script type="text/javascript">
      //Start the main timer
      console.time('DOMContentLoaded');
    </script>
  </head>
  <body>
    <p>PAGE CONTENT GOES HERE</p>
    <script type="text/javascript">
      function afterDOMContentLoadedEvent() {
        //Stop the time after the DOMContentLoaded event
        console.timeEnd('DOMContentLoaded');  
      }
    </script>
  </body>
</html>
{% endhighlight %}

### Establishing the Baseline

Next we tested the page load time in various browsers. The page we tested is 
the [translation for test][test]. This is one of the more complex pages on 
the site. Here is what we found:

![Baseline Performance]({{ img_dir }}/chart_baseline.png)

	Chrome17: 179ms
	FF9:      300ms
	FF3.6:	  500ms
	IE9: 	  684ms
	IE8:	  462ms

Wow. That is a lot of time rendering--almost 10 times as much time as it 
takes for the server to generate the page. This finding resonates with the
[Performance Golden Rule][souders] from Steve Souders, which is that 80-90% of
the end-user response time is spent on the front end.

### Back to Basics 

Next, we stripped down the page and started with the barebones HTML--no CSS, 
no JS--and measured again. The gap between these two represents the 
opportunity for front-end optimizations. And it's big. Here are the results:

![No JS / No CSS Performance]({{ img_dir }}/chart_nojs_nocss.png)

	Chrome17: 20ms (129ms gap)
	FF9:      50ms (250ms gap)
	FF3.6:	  134ms (366ms gap)
	IE9: 	  125ms (559ms gap)
	IE8:	  130ms (332ms gap)

Now let's add back CSS, but exclude the JS:

![No JS Performance]({{ img_dir }}/chart_nojs.png)

	Chrome17: 61ms (41ms gap)
	FF9:      129ms (79ms gap)
	FF3.6:	  316ms (182ms gap)
	IE9: 	  415ms (290ms gap)
	IE8:	  411ms (281ms gap)

![No CSS Performance]({{ img_dir }}/chart_nocss.png)

Now let's include the JS, but exclude the CSS:

	Chrome17: 131ms (111ms gap)
	FF9:      211ms (161ms gap)
	FF3.6:	  450ms (316ms gap)
	IE9: 	  331ms (206ms gap)
	IE8:	  180ms (50ms gap)

We can see that we have a lot of opportunity to improve both the JS and the 
CSS on the site. Now let's dive into the improvements. 

<!-- more start -->

### A Big JS Improvement...in a Flash

We used [DynaTrace Ajax 3][dynatrace] to identify the bottlenecks in Internet 
Explorer.  We found that a major culprit was [SoundManager2][soundmanager], a 
library that allows us to play audio files.

In the background, SoundManager loads a flash movie if HTML5 audio is not 
available. This can significantly slow rendering time as the browser must 
[negotiate with Flash](http://www.html5rocks.com/en/tutorials/speed/html5/) 
to render the display output for the page. So our javascript library was
loading a flash component--and flash cause major slow downs. We changed the 
code so that SoundManager only loads after a user clicks on the audio icon. 
Removing SoundManager resulted in a nearly 100ms improvement in IE. That was
one of our larger changes.

### CSS - It's element{s}ary my dear Watson

We also had to tackle the CSS delays. Using DynaTrace, we noticed that IE was
spending an inordinate amount of time [rendering the page][ierendering]. To 
find out why, we had to test removing various parts of our CSS. One biggest 
drain on performance turned out to be the CSS reset, which is based on 
[normalize.CSS](http://necolas.github.com/normalize.CSS/).  In IE, the CSS 
reset alone created a 100ms delay. We were testing a complex page with over 
1500 elements, and the reset applies to virtually all of them. The 
[DOM Monster](http://mir.aculo.us/dom-monster/) profiling tool was begging 
for fewer elements. And it was right. On a simple page, the penalty for the 
reset was only 20ms. 

Digging deaper, the elements on the page seemed to play a major role in 
the IE rendering time. The homepage, which has relatively few elements, 
loaded in 160ms, rather than the 415ms seen when the page had a lot of 
elements. The solution here is to delay loading of many elements until a user
scrolls down to see them. Delaying the loading of a large dictionary result 
could speed up the initial response by over 100ms. As a result, we decided to 
pre-load fewer elements on the page, allowing certain sections to only load
after a user made an ajax call to retrieve the elements. 

Another CSS optimization that we did was run [Google Pagespeed][pagespeed] and
identify the slow CSS rules in our code. Google Pagespeed is able to identify
any rules that browsers struggle to execute. In our case, because we had so 
many elements on the page, the impact of each slow rule was magnified
significantly. 

### You Get What you Measure

This project made apparent that for our site, front-end performance is a
key metric that we must measure, monitor, and manage. Performance optimization
is an ongoing effort. We embedded within our code an easy way to measure 
across browsers the frontend load time of any page on our site. We also 
elevated the importance of the 
[site speed report][analytics] that is available in Google Analytics on our
metrics dashboard. These tools allow us to regularly monitor the impact of 
changes on our frontend performance to ensure that we maintain a zippy
user response time as we make changes to the site. 


[speedracer]: http://en.wikipedia.org/wiki/Speed_Racer
[shopzilla]: http://www.scribd.com/doc/16877317/Shopzillas-Site-Redo-You-Get-What-You-Measure
[kissmetrics]: http://blog.kissmetrics.com/loading-time/?wide=1
[webmastertools]: http://googlewebmastercentral.blogspot.com/2010/04/using-site-speed-in-web-search-ranking.html
[test]: http://www.spanishdict.com/translate/test
[crossbrowser]: https://developer.mozilla.org/en/DOM/element.addEventListener
[dynatrace]: http://ajax.dynatrace.com/ajax/en/
[chromedev]: http://code.google.com/chrome/devtools/docs/profiles.html
[firebug]: http://getfirebug.com/
[souders]: http://www.stevesouders.com/blog/2012/02/10/the-performance-golden-rule/
[soundmanager]: http://www.schillmania.com/projects/soundmanager2/
[ierendering]: http://blog.dynatrace.com/2009/12/12/understanding-internet-explorer-rendering-behaviour/
[pagespeed]: http://code.google.com/speed/page-speed/
[yslow]: http://developer.yahoo.com/yslow/
[webpagetest]: http://www.webpagetest.org/
[console]: http://stackoverflow.com/questions/3516515/console-time-in-ie8-developer-tools
[analytics]: http://analytics.blogspot.com/2011/12/greater-insights-from-site-speed-report.html
[pagespeed]: http://code.google.com/speed/page-speed/docs/using_chrome.html