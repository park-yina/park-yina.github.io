---
layout: default
title: C언어
permalink: /categories/C/
taxonomy: C언어
---
{% assign C = site.categories.c%}

<h1 style="margin-left: 10px;">C언어 정리</h1>
<hr>
<div class="entries-{{ entries_layout }}" style="margin-left: 30px;">
  <ul>
    {% for post in C %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>