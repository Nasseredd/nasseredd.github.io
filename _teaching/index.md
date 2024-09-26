---
layout: archive
title: "Teaching"
permalink: /teaching/
author_profile: true
---

<!-- {% for course in site.teaching %}
  {% if course.path contains '/index.md' and course.url != page.url %}
    <h2><a href="{{ course.url | relative_url }}">{{ course.title }}</a></h2>
    <p>{{ course.description }}</p>
  {% endif %}
{% endfor %} -->

{% for course in site.teaching %}
  {% unless course.path contains 'practical' %}
    <h2><a href="{{ course.url | relative_url }}">{{ course.title }}</a></h2>
    <p>{{ course.description }}</p>
  {% endunless %}
{% endfor %}