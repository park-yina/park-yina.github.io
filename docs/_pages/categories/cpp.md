---
layout: default
title: cpp Posts
permalink: /categories/kotlin
taxonomy: cpp
---
<style>
  ul {
    margin-left: 40px;  // 여백 조절
  }
</style>
<div class="sidebar sticky">
<h1>cpp</h1>
<hr>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
</div>
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories.kotlin %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>
