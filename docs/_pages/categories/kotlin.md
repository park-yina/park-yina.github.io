---
layout: default
title: Kotlin Posts
permalink: /categories/kotlin
taxonomy: kotlin
---
<style>
  ul {
    margin-left: 40px;  // 여백 조절
  }

  ul a {
    color: #5627a8;  // 하이퍼링크 색상 변경
  }
</style>
<h1>📱Koltin</h1>
<hr>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
<div class="entries-{{ entries_layout }}">
<h1>스터디 자료</h1>
  {% for post in site.categories.kotlin %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>