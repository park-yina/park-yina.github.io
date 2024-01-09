---
layout: default
title: 크래프톤 정글
permalink: /categories/jungle/
taxonomy: jungle
---
{% assign jungle_posts = site.categories.jungle %}

<h1 style="margin-left: 10px;">📌크래프톤 정글</h1>
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