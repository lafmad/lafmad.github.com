---
title:
layout: page
---

<ul class="listing">
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% capture m %}{{post.date | date:"%M"}}{% endcapture %}
  {% if year != y and month != m %}
    {% assign year = y %}
    {% assign month = m %}
    <li class="listing-seperator">{{ y }-{ m }}</li>
  {% endif %}
  <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>
