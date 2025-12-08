---
title: Projects
layout: default
permalink: /projects/
---

<ul style="list-style:none;padding-left:0">
{% assign items = site.projects | sort: "weight" | sort: "date" | reverse %}
{% for p in items %}
  {% include project-card.html p=p %}
{% endfor %}
</ul>

