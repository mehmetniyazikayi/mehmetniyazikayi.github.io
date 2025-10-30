---
title: "Tag: QAOA"
permalink: /tags/qaoa/
---

# Tag: QAOA

<ul>
{% for p in site.projects %}
  {% if p.tags contains "qaoa" %}
    <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>

