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
  <ul style="display: flex; flex-wrap: wrap;">
    {% for post in jungle_posts %}
      <li style="list-style: none; margin-bottom: 10px; width: calc(50% - 5px);"> <!-- 아이템의 너비 조절하여 한 줄에 두 개씩 배치 gpt찬스 씀 -->
      {% if post.header.teaser %}
      <img src="{{ post.header.teaser }}" alt="Teaser Image" style="max-width:100px;">
      {% endif %}
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>
