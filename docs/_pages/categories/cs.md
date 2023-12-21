---
layout: default
title: CS 그리고 알고리즘
permalink: /categories/cs/
taxonomy: cs
---
<h1 style="
    margin-left: 10px;
">🖥CS와 알고리즘(이론)에 대해 정리하는 카테고리입니다</h1>
<hr>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
<div class="entries-{{ entries_layout }}"
style="margin-left: 30px;">
  {% for post in site.categories.cs %}
    <h2><a href="{{ post.url }}">{{ post.title }}
  {% endfor %}