---
layout: page
title: Sailing
permalink: /sailing/
---

<ul>
  {% for post in site.posts %}
    {% if post.categories contains "sailing" %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <small>{{ post.date | date: "%B %d, %Y" }}</small>
      </li>
    {% endif %}
  {% endfor %}
</ul>