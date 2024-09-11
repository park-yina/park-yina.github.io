---
layout: default
title: 프로젝트
permalink: /categories/project/
taxonomy: project
pagination:
  enabled: true
  category: project
---

{% assign project_posts = site.categories.project %}

<h1 style="margin-left: 10px;">프로젝트</h1>
<hr>
<div class="entries-{{ entries_layout }}" style="margin-left: 30px;">
  <ul style="display: flex; flex-wrap: wrap;">
    {% for post in paginator.posts %}
      <li style="list-style: none; margin-bottom: 10px; width: calc(50% - 5px);">
      {% if post.header.teaser %}
      <img src="{{ post.header.teaser }}" alt="Teaser Image" style="max-width:100px;">
      {% endif %}
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>

{% include paginator.html %}
