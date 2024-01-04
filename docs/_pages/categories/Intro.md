---
layout: default
title: Blog아카이브
permalink: /categories/Intro
taxonomy: Blog
---
{% assign blog_posts = site.categories.Intro %}

<h1 style="margin-left: 10px;">블로그 아카이브</h1>
<hr>
<div class="entries-{{ entries_layout }}" style="margin-left: 30px;">
  <ul>
    {% for post in liter_posts %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>