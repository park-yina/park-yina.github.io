---
layout: default
title: CS
permalink: /categories/cs/
pagination:
  enabled: true
  category: cs
---
<div class="card-container" style="display: flex; flex-wrap: wrap; margin-left: 30px;">
  {% for post in paginator.posts %}
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
      <p class="card-summary" style="margin: 10px 0;">{{ post.summary }}</p>
    </div>
  </div>
  {% endfor %}
</div>
<nav class="pagination">
  <div class="pagination__wrapper">
    <h2 class="is-blind">포스트 페이지 매김</h2>
    {% if paginator.previous_page %}
      <a href="{{ paginator.previous_page_path | prepend: site.baseurl }}" class="pagination__anchor pagination__anchor--prev">이전 페이지</a>
    {% else %}
      <span role="link" aria-disabled="true" class="pagination__anchor pagination__anchor--prev is-disabled">이전 페이지</span>
    {% endif %}
    {% if paginator.next_page %}
      <a href="{{ paginator.next_page_path | prepend: site.baseurl }}" class="pagination__anchor pagination__anchor--next">다음 페이지</a>
    {% else %}
      <span role="link" aria-disabled="true" class="pagination__anchor pagination__anchor--next is-disabled">다음 페이지</span>
    {% endif %}
    <ul class="pagination__list">
      {% if paginator.page_trail %}
        {% for trail in paginator.page_trail %}
          <li class="pagination__listitem">
            {% if page.url == trail.path %}
              <em role="link" aria-disabled="true" aria-label="현재 페이지, {{ trail.num }}번 페이지" aria-current="page" class="pagination__anchor is-active">{{ trail.num }}</em>
            {% else %}
              <a href="{{ trail.path | prepend: site.baseurl | replace: 'index.html', '' }}" aria-label="{{ trail.num }}번 페이지" class="pagination__anchor">{{ trail.num }}</a>
            {% endif %}
          </li>
        {% endfor %}
      {% endif %}
    </ul>
  </div>
</nav>
