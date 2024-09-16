---
layout: default
title: CS 그리고 알고리즘
permalink: /categories/cs/
pagination: 
  enabled: true
taxonomy: cs
---
{% assign project_posts = paginator.posts %}

<div class="card-container" style="display: flex; flex-wrap: wrap; margin-left: 30px;">
  {% for post in project_posts %}
  <div class="card" style="width: calc(50% - 20px); margin: 10px; border: 1px solid #ddd; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);">
    {% if post.header.teaser %}
    <div class="card-image" style="max-height: 200px; overflow: hidden;">
      <img src="{{ post.header.teaser }}" alt="Teaser Image" style="width: 100%; object-fit: cover;">
    </div>
    {% endif %}
    <div class="card-content" style="padding: 15px;">
      <h2 style="font-size: 18px; margin: 0;">
        <a href="{{ site.baseurl }}{{ post.url }}" style="text-decoration: none; color: #333;">{{ post.title }}</a>
      </h2>
    </div>
  </div>
  {% endfor %}
</div>

{% include paginator.html %}
