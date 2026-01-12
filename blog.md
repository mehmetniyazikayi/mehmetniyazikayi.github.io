---
title: Blog
layout: default
permalink: /blog/
---
{% include blog-intro.html %}

{% assign posts_list = paginator.posts | default: site.posts %}

<ul>
  {% for post in posts_list %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small> — {{ post.date | date: "%Y-%m-%d" }}</small>
    </li>
  {% endfor %}
</ul>

{% if paginator %}
<nav>
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | relative_url }}">Newer</a>
  {% endif %}
  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | relative_url }}">Older</a>
  {% endif %}
</nav>
{% endif %}
