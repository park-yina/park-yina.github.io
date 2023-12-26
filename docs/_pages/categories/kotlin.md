---
layout: default
title: Kotlin Posts
permalink: /categories/kotlin/
taxonomy: kotlin
---
{% assign kotlin_posts = site.categories.kotlin %}

<h1 style="margin-left: 10px;">📱Kotlin</h1>
<hr>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>
<div class="entries-{{ entries_layout }}" style="margin-left: 30px;">
  <ul>
    {% for post in kotlin_posts %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>
