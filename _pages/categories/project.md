---
layout: default
title: project
author_profile: true
permalink: /categories/project/
pagination:
  category: project
  enabled: true
  per_page: 12
  sort_reverse: true
  trail:
    before: 2
    after: 2
---

<div class="card-container" style="display: flex; flex-wrap: wrap; justify-content: space-between; margin-left: 10px; margin-right: 10px;">
  {% for post in paginator.posts %}
  <div class="card" style="width: calc(33.333% - 20px); margin: 10px; border: 1px solid #ddd; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);">
    {% if post.header.teaser %}
    <div class="card-image" style="max-height: 200px; overflow: hidden;">
      <img src="{{ post.header.teaser }}" alt="Teaser Image" style="width: 100%; object-fit: cover;">
    </div>
    {% endif %}
    <div class="card-content" style="padding: 15px;">
      <h2 style="font-size: 18px; margin: 0;">
        <a href="{{ site.baseurl }}{{ post.url }}" style="text-decoration: none; color: #333;">{{ post.title }}</a>
      </h2>
      <p class="card-summary" style="margin: 10px 0;">{{ post.summary }}</p>
    </div>
  </div>
  {% endfor %}
</div>
{% include paginator-project.html %}
