---
title: Blog
permalink: /blog/
---

# Blog
{% include blog-intro.html %}

<ul>
  {% for post in paginator.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small> — {{ post.date | date: "%Y-%m-%d" }}</small>
    </li>
  {% endfor %}
</ul>

<nav>
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | relative_url }}">Newer</a>
  {% endif %}
  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | relative_url }}">Older</a>
  {% endif %}
</nav>

