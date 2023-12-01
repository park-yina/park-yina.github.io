---
layout: default
title: Kotlin Posts
permalink: /categories/kotlin
taxonomy: kotlin
---
<style>
  ul {
    margin-left: 40px;  // 여백 조절
  }

  ul a {
    color: #5627a8;  // 하이퍼링크 색상 변경
  }
</style>
<h1>  📖코틀린 스터디</h1>
<content>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</content>

<div class="{{ include.type | default: 'list' }}__item">
  <article class="archive__item" itemscope itemtype="https://schema.org/CreativeWork">
    <div>
      <span>
        <a href="{{ post.url }}">{{post.title}}</a>
      </span>
      <small> 
        <i class="fas fa-fw fa-calendar-alt" aria-hidden="true"> </i>{{ post.date | date: " %Y.%m.%d" }}
        {% if site.category_archive.type and post.categories[0] and site.tag_archive.type and post.tags[0] %}
          {%- include post__taxonomy.html -%}
        {% endif %}
      </small>
    </div>
  </article>
</div>

<div class="entries-{{ entries_layout }}">
  {% for post in pages.categoires.kotlin %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  {% endfor %}
</div>
