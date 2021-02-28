---
title: "Contents"
layout: default
---

<header>
  <h1>Contents</h1>
</header>

{% for collection in site.collections %}
  {% if site[collection.label] != empty %}
  <h2 class="collection-title">{{ collection.title }}</h2>
  <hr class="fading" style="width: 33%;">
  <ul style="list-style-type: none; padding-inline-start: 0;">
  {% for page in site[collection.label] %}
    <li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
  {% endfor %}
  </ul>
  {% endif %}
{% endfor %}

