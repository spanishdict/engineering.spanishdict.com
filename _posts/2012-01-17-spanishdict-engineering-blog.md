---
layout: post
author: Ryan Roemer
author_link: https://github.com/ryan-roemer
author_email: ryan@spanishdict.com
title: Our New Engineering Blog!
description: We've launched a new engineering blog for all things technical at
  SpanishDict.com. Our site is developed using the Jekyll static site
  generator, and hosted on GitHub's awesome Pages service.
date: 2012-01-17 14:00:00 UTC
tags: ['spanishdict', 'engineering', 'blog', 'github', 'jekyll']
---

## Engineering at the World Leader in Spanish Learning

At [SpanishDict][sd], our engineering team works daily with a number of cool
search, natural language, database, cloud and web technologies. We thought it
was about time to let the world peer in a bit at how we work and what we do
here to support our reference / translation services and various language
learning tools.

The first step in this direction is to offer a blog, and as a fitting first
post, we'll discuss what technologies we chose and why.

## Blogging Options Everywhere

There are an enormous amount of great blogging resources out there for
technically-focused blogs like ours, ranging from lightweight
[Posterous][posterous], to the venerable [Blogger][blogger] platform.

After some discussion of the world of blogs and features, we honed down our
use cases for our blog to the following:

* **Lightweight Editing**: We need editing to be an "easy" task, ideally in
  a language like [Markdown][markdown] and most certainly in text, not HTML.
  I personally don't like editing to necessitate being online, so an offline
  editing capability would be nice too.
* **Versioning/Collaboration**: We'd like to be able to version the blog and
  allow collaborative editing without authors stepping on each others' toes.
  Having the full blog under git would be a great way to do both versioning
  and control.
* **Syntax Highlighting**: We're developers, we speak code, we need to show
  all of our awesome programs in a highlighted, usable manner.

## Jekyll and GitHub Pages = Geek Heaven

After a good amount of research and experimentation with a number of blog
platforms, we arrived at a solution that squarely hit all of our use cases:
[GitHub][gh] and [Jekyll][jekyll].

<!-- more start -->

Jekyll is a static website generator technology that defines conventions for
a website, and gives the user control over:

* **Layouts**: Defining the look and feel of the entire site with a template
  language.
* **Posts**: Supports blog posts with a convention system that makes writing a
  new post as simple as adding a new text file.
* **Static Media**: Jekyll supports basic static media hosting as well. We have
  full control over whatever CSS / images we want to serve up.

Jekyll essentially lets a developer generate practically any site they want,
with some shortcuts for blog posts, etc. if you use the conventional support
(which we do). Other niceties in Jekyll include:

* **Markdown Support**: Jekyll supports Markdown along with other
  pre-processing language options. This is great for us, as Markdown is one
  of the core documentation languages for developers, and doesn't affect the
  resulting HTML output, so we can change internal HTML structure (in our
  layout templates) without having to change all of our posts / pages later.
* **Git Repository / Source Code**: Our Jekyll site corresponds to a git
  repository on our GitHub account. This allows all of our developers to
  collaboratively edit the site, and handle simultaneous edits / conflicts
  as just another git merging task.
* **GitHub Support**: GitHub will actually build a website using Jekyll if
  you correctly configure a magic "`gh-pages`" git branch. Since we already
  host our repositories on GitHub, this is a no-brainer.
* **Offline Support**: We can build the full Jekyll site on a local computer
  with no internet connection, giving our developers lots of flexibility in
  terms of being able to jot down thoughts and add enhancements to the blog
  whenever they want, without having to route everything through a blog
  platform online administrative interface.

## ... and Back to Work.

We iterate and release often at SpanishDict. And that also applies to our blog.
Now that we're live, we'll be tinkering and' playing with the look and feel
until it truly feels like our new "home". Let us know what you think!

As a final note, we are looking for developers to round out our engineering
team. We're a fun and growing group, located in the DC metro area / Northern
Virginia, and work with a modern array of web, search, cloud and data store
technologies. Come [join us][sd_jobs]!

[blogger]: http://www.blogger.com/
[gh]: https://github.com/
[jekyll]: http://jekyllrb.com/
[markdown]: http://daringfireball.net/projects/markdown/
[posterous]: https://posterous.com/
[sd]: http://www.spanishdict.com/
[sd_jobs]: http://www.spanishdict.com/careers

<!-- more end -->
