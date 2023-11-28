 ---
 title: "📗개발도서 뿌시기"
 layout: archive
 permalink: /categories/develop/
 author_profile: true
 sidebar:
   nav: "docs"
 ---
 {% assign posts = site.categories.categories %}
 {% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}