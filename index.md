---
layout: default
title: Home
---

{% for post in site.posts limit:5 %}
<div class="inner">
  <div class="post">
    {% include post_header.html %}
    {% include post_meta.html %}
    <div class="excerpt">
      {{ post.content | replace: '--', 'DOUBLE_DASH' | replace: '<!DOUBLE_DASH', '<!--'  | replace: 'DOUBLE_DASH>', '-->' | replace:'DOUBLE_DASH','&endash;&endash;' | replace:'more start -->','' | replace:'<!-- more end','' }}
    </div>
    <div class="more">
      Read <a href="{{ post.url }}">more</a>...
    </div>
  </div>
</div>
{% endfor %}
