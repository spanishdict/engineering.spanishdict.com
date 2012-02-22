---
layout: post
author: Ryan Roemer
author_link: https://github.com/ryan-roemer
author_email: ryan@spanishdict.com
title: Async.js Talk for Joint Node.DC / DC jQuery Meetup
description: Nested callbacks and control flow complicate and plague the lives
  of front- and back-end developers. Async.js is a control flow library that
  offers solid abstractions to handle asynchronous logic intelligently and
  succinctly. Ryan discusses this wonderful library in the Feb. 20, 2012 joint
  meetup for Node.DC and DC jQuery.
date: 2012-02-22 15:27:00 UTC
tags: ['javascript', 'control flow', 'node.js', 'async.js', 'parallel']
---
{% capture img_dir %}{{ site.baseurl }}media/img/{{page.date|date: "%Y/%m/%d"}}{% endcapture %}

## DC Node/jQuery Presentation

I gave the following presentation on Async.js to a combined [Node.DC][node_dc]
and [DC jQuery][dcjq] meetup on Feb. 20, 2012.

[![Async.js presentation][img_pres]][pres]
[img_pres]: {{ img_dir }}/async-talk.png

The full [presentation][pres] is available on GitHub, and uses the
[Impress.js][impress] CSS3-based presentation framework. Consequently, it
might not render well in older browsers and IE.

## Better JavaScript Control Flow with Async.js

[Async.js][asyncjs] is a control flow library for the browser and
[Node.js][nodejs]. It is a wonderful tool for taming parallel, serial and
dependency graph-like combinations of asynchronous callbacks. Put another way,
if this nested-callback pattern looks familiar:

{% highlight javascript %}
fun1(params, function (err, results) {
  fun2(params, function (err, results) {
    fun3(params, function (err, results) {
      fun4(params, function (err, results) {
        fun5(params, function (err, results) {
          fun6(params, function (err, results) {
            // Do something interesting here.
          });
        });
      });
    });
  });
});
{% endhighlight %}

then Async.js might just be your solution.

<!-- more start -->

## Async.js Features

My talk covers some of Async.js' most fundamental abstractions:

* Series
* Waterfall
* Parallel
* Collections

However, there are many, many more functions and helper methods to deal with
a diverse array of concurrent / asynchronous development problems, so I
strongly encourage a thorough reading of the library's [README][asyncjs] to
see what's available and review the great examples provided along with the
library.

[nodejs]: http://nodejs.org/
[asyncjs]: https://github.com/caolan/async
[node_dc]: http://www.meetup.com/node-dc/events/49905452/
[dcjq]: http://www.meetup.com/DC-jQuery-Users-Group/events/51798912/
[pres]: http://ryan-roemer.github.com/nodedc-async-talk/#/title
[impress]: http://bartaz.github.com/impress.js
[prezi]: http://prezi.com/

<!-- more end -->
