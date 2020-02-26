---
layout: page
title: Blog
permalink: /blog/
---

I will try to write on various topics of my interest here. Although the purpose of all these blogs is practice improve my writing skills. Bioinformatics topic that you will find here mostly for my own documentations but might be helpful for you too.  You can also search my posts by category <a href="{{ site.baseurl }}/categories/">here</a>.

<ul class="listing">
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <li class="listing-seperator">{{ y }}</li>
  {% endif %}
  <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>
