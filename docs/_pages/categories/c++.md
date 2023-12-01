---
layout: default
title: c++풀기
permalink: /categories/cpp
taxonomy: c++
---
<style>
  ul {
    margin-left: 40px;  // 여백 조절
  }

  ul a {
    color: #5627a8;  // 하이퍼링크 색상 변경
  }
</style>
<div class="sidebar sticky">
<h1>  📖코틀린과 스터디</h1>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
</div>
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories.kotlin %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories.cpp%}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>
