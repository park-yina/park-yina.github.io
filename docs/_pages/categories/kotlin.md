---
layout: default
title: Kotlin Posts
permalink: /categories/kotlin
taxonomy: kotlin
---
<h1 style="
    margin-left: 10px;
">📱Koltin</h1>
<hr>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
<div class="entries-{{ entries_layout }}"
style="margin-left: 30px;">
<h1>스터디 자료</h1>
  {% for post in site.categories.kotlin %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>