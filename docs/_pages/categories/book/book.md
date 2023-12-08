---
layout: default
title: 📚책과 스터디
permalink: /categories/book
category: book  # '📚책과 스터디' 대신에 'book'으로 변경
---
<h1 style="
    margin-left: 10px;
">Book</h1>
<hr>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
<div class="entries-{{ entries_layout }}"
style="margin-left: 30px;">
<h1>📚개발도서</h1>
  {% for post in site.categories.book %}
    <h2><a href="{{ post.url }}">{{ post.title }}
  {% endfor %}