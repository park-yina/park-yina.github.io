---
layout: default
title: 📚책과 스터디
permalink: /categories/book
category: book  # '📚책과 스터디' 대신에 'book'으로 변경
---
<style>
  ul {
    margin-left: 40px;  // 여백 조절
  }

  ul a {
    color: #5627a8;  // 하이퍼링크 색상 변경
  }
</style>
<h1>  📖책과 스터디 게시물</h1>
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories['book'] %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>