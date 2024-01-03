---
layout: default
title: Liter
permalink: /categories/Liter
taxonomy: kotlin
---
{% assign liter_posts = site.categories.Liter %}

<h1 style="margin-left: 10px;">📚문학에 대한 기록</h1>
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