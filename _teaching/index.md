---
layout: archive
title: "Teaching"
permalink: /teaching/
author_profile: true
---

{% assign courses = site.teaching | where_exp: "item", "item.collection_type == 'course'" %}
{% for course in courses %}
  <h2><a href="{{ course.url | relative_url }}">{{ course.title }}</a></h2>
  <p>{{ course.description }}</p>
{% endfor %}