---
layout: default
title: 📚책과 스터디
permalink: /categories/book
category: book  # '📚책과 스터디' 대신에 'book'으로 변경
---
{% assign book_posts = site.categories.book %}

<h1 style="margin-left: 10px;">📌개발도서 읽기</h1>
<hr>
<div class="entries-{{ entries_layout }}" style="margin-left: 30px;">
  <ul>
    {% for post in book_posts %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>
