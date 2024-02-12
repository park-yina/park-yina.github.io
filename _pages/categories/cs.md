---
layout: default
title: CS 그리고 알고리즘
permalink: /categories/cs/
taxonomy: cs
---
{% assign cs_posts = site.categories.cs %}

<h1 style="margin-left: 10px;">📌알고리즘AND이론</h1>
<hr>
<div class="entries-{{ entries_layout }}" style="margin-left: 30px;">
  <ul>
    {% for post in cs_posts %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>