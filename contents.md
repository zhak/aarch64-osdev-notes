---
title: "contents"
layout: default
---

<header>
  <h1>Contents</h1>
</header>

<ul style="list-style-type: none; padding-inline-start: 0;">
  {% for page in site.pages %}
    {% if page.layout == 'note' %}
      <li>
        <a href="{{ page.url | relative_url }}">{{ page.title }}</a>
      </li>
    {% endif %}
  {% endfor %}
</ul>
