---
layout: post
author: Zach Cross
author_link: https://github.com/zcross
title: My SpanishDict Internship
description: A brief discussion of my summer internship
date: 2012-07-25 12:30:00 UTC
tags: ['interns', 'careers', 'spanishdict.com', 'washington, dc']
---

{% capture img_dir %}{{ site.baseurl }}media/img/{{page.date|date: "%Y/%m/%d"}}{% endcapture %}

My name is Zach Cross, and I am currently an intern at SpanishDict. In a few
days, I will be returning to Chapel Hill, North Carolina to finish my last
year of undergrad at UNC, where I study Computer Science. The goal of this
post is to reflect on my experience at SpanishDict, both for my own benefit
and for communicating what it’s like to work at this great company.

[![My workspace][zach_photo]]

[zach_photo]: {{ img_dir }}/zach_mugshot.png

I started here with two other interns (Hari Ganesan and Maria Bajzek) in late
May. Moving from rural North Carolina to Washington, DC was an interesting
transition, but I quickly settled into a comfort zone both at work and in the
city. We have a company culture that creates a low stress, personal atmosphere
that encourages productivity and helps us achieve our ambitious goals. From
day one, I have learned an increasing amount about the company, our product,
and the people here. In the context of engineering, I have benefited from the
torrent of knowledge that is Ryan Roemer, our Director of Engineering. I have
learned not only as a direct result of my project work, but also in asking
Ryan questions about his own work. Additionally, I have learned about our
business model through our weekly team meetings and in everyday conversations
with other members of the team.

My primary project relates to both managing changes to the schema of our
database in response to regular changes to the website (especially with the
addition of our Node.js API) and maintaining the quality of our content. The
fundamental problem I sought out to solve was managing database state (both
schema and data) in a flexible, controlled manner that still allowed for
sweeping changes. The secondary problem was creating a better interface to our
database for content maintainers.

To solve this problem, I used the Django web framework with the Django app
South for data and schema migrations. Because I wasn’t working with a clean
slate -- that is, the database already existed -- I relied on Django’s
database introspection tools and some manual (and scripted) tweaks to model
our data. Several iterations of work later, a handy schema diff tool confirmed
that my Django models captured the schema of the current database properly.
From there, I modified Django’s built-in admin web interface to suit our
needs. We now have a number of schema and data migrations in the teens, in
response to needs for new features and data quality control. That is the long
and short of it, but I should say that using Django’s ORM (object relational
mapper) to programmatically handle data migrations was much more convenient
than sanitizing and validating huge batches of SQL commands.

Having very much simplified my primary project in this post, I do want to
elaborate on one particular set of migrations I worked on. We are a data-
driven company, with tons of log data at both the application and server
levels. I wrote a few data and schema migrations to facilitate the viewing of
user query data via the admin web interface I mentioned. In addition, I wrote
a few normalizations for our Hadoop MapReduce jobs that boiled down our logs
into feasible quantities. The exposure to big data (something that once seemed
nebulous) was a great learning opportunity, although it was pretty easy given
our in-house tools for big data analytics. Now, we have the capability for
team members who aren’t developers to add and make changes to our site
content. Most importantly, we can react to what our users are searching for
and better serve their needs. The web interface reflecting this analytics data
was also constructed in such a way that progress is trackable without hassle.

As I wrapped up my primary project, I asked Chris (our CEO and a fellow
developer) if there was more project work that needed to be done. He gave me
two terrific projects related to a new product of ours... but I can’t go into
detail on that just yet! The point is that there is always exciting work to do
at SpanishDict, that we are continually seeking to improve our existing and
new products. This sense of zero stagnation is probably one of the best parts
of working here. New features are being created every day, and old ones are
being improved. Not to mention, there is no shortage of ideas between our
brilliant team members!

For anyone considering working here, whether or not you are a developer, if
you are looking for exciting work and great co-workers, look no further! We
have great people, great products, and great purpose! Y para los que hablan
español, o quieren aprender, tengo que decir que esta oficina está llena de
gente cosmopolita que traen todo tipo de experiencias internacionales y
culturales al equipo. ¡Hay mucho que compartir y aprender!

And for the developer-types considering working at SpanishDict, know that
there is an abundance of challenging (and therefore fun) problems to solve.
That and very intelligent and creative coworkers who will no doubt be a source
of knowledge and motivation. To end this post, I’ll throw some technology
buzzwords to capture some of what I’ve seen and learned about (in varying
degrees) at work:

Django, Python, Boto, MySQL, PHP, MrJob, Node.js, Coffeescript, Loggly, Scout,
NoSQL, MongoDB

[spanishdict]: http://www.spanishdict.com
