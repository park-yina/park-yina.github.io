---
layout: default
title: Kotlin Posts
permalink: /categories/kotlin
taxonomy: kotlin
---
{% assign posts = pages.categories.kotlin %}
{% for post in posts %}
  {% if post.header.teaser %}
    {% capture teaser %}{{ post.header.teaser }}{% endcapture %}
  {% else %}
    {% assign teaser = site.teaser %}
  {% endif %}

  {% if post.id %}
    {% assign title = post.title | markdownify | remove: "<p>" | remove: "</p>" %}
  {% else %}
    {% assign title = post.title %}
  {% endif %}

  {% include custom-archive-single.html type=entries_layout %}

{% endfor %}