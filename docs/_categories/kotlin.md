---
layout: default
title: Kotlin
permalink: /categories/coding/kotlin/
---

<h1>Posts in the Kotlin category under Coding</h1>

{{ content }}

{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {% for post in site.categories['coding/kotlin'] %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>
