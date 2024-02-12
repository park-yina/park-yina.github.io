---
layout: default
title: cpp Posts
permalink: /categories/cpp
taxonomy: cpp
---
<style>
  ul {
    margin-left: 40px;  // 여백 조절
  }
</style>
<h1>cpp</h1>
<hr>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories.cpp %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>