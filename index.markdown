---
title:
layout: page
---

<ul class="listing">
 {% for post in site.posts  %}
 {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
 {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
 {% capture this_month_num %}{{ post.date | date: "%m" }}{% endcapture %}
 {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
 {% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
 {% capture next_month_num %}{{ post.previous.date | date: "%m" }}{% endcapture %}

 {% if forloop.first %}
 <h2><a class="blog_sidebar_header" href="/#">{{this_year}}</a></h2>
 <h3><a href="/#">{{this_month}}</a></h3>
 <ul>
   {% endif %}
   <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
  {% if forloop.last %}
</ul>
<div class="clear padding30"></div>
{% else %}
{% if this_year != next_year %}
</ul>
<div class="clear padding30"></div>
<h2><a class="blog_sidebar_header" href="/#">{{next_year}}</a></h2>
<h3><a href="/#">{{next_month}}</a></h3>
<ul>
  {% else %}
  {% if this_month != next_month %}
</ul>
<div class="clear padding30"></div>
<h3><a href="#">{{next_month}}</a></h3>
<ul>
 {% endif %}
 {% endif %}
 {% endif %}
 {% endfor %}

 {% assign posts_collate = null %}
</ul>
