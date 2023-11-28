---
layout: categories
title: Kotlin Posts
permalink: /categories/kotlin
taxonomy: kotlin
---
<h1>  🗃Kotlin 게시물</h1>
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories['kotlin'] %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>