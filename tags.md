---
title: Tags
permalink: /tags/
---

# Tags

{% assign all = site.projects | map: 'tags' | compact | join: ',' | split: ',' | uniq | sort %}
<ul>
{% for tag in all %}
  {% assign slug = tag | downcase | replace: ' ', '-' %}
  <li><a href="{{ '/tags/' | append: slug | append: '/' | relative_url }}">{{ tag }}</a></li>
{% endfor %}
</ul>

