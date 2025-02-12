---
layout: page
title: Growth
permalink: /growth/
---

<ul>
  {% for post in site.posts %}
    {% if post.categories contains "growth" %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <small>{{ post.date | date: "%B %d, %Y" }}</small>
      </li>
    {% endif %}
  {% endfor %}
</ul>