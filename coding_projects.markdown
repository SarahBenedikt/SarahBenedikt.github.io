---
layout: page
title: Coding
permalink: /projects/
---

<ul>
  {% for post in site.posts %}
    {% if post.categories contains "coding" %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
        <small>{{ post.date | date: "%B %d, %Y" }}</small>
      </li>
    {% endif %}
  {% endfor %}
</ul>