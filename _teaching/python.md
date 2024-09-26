<!-- ---
title: "Introduction to Python (Practicals)"
collection: teaching
collection_type: course
permalink: /teaching/python/
venue: "Université de Lorraine, IDMC"
date: 2024-09-01
location: "Nancy, France"
description: "These Python practicals follow the lectures of [Karën Fort](https://members.loria.fr/KFort/idmc-nancy-from-2024/). Throughout the course, you will be introduced to Python, starting with foundational concepts such as strings, control flow, and loops. You'll then explore lists, tuples, sets, and file handling, with practical exercises like working on the "80jours50l" file. As we progress, you'll dive into dictionaries and functions using the "MyBiblio" file, followed by a recap to reinforce your learning. After that, we'll cover Python modules, how to use Python outside of Jupyter notebooks, and introduce essential libraries like NumPy and Pandas. We'll conclude with a brief session on objects. Each topic comes with interactive notebooks to ensure hands-on practice. I will be supervising one group of these sessions, guiding you through the exercises and helping you strengthen your Python skills."
---

{{ content }}

<h2>Practicals</h2>
<ul>
{% assign practicals = site.teaching | where_exp: "item", "item.path contains 'python/' and item.path contains 'practical'" %}
{% for practical in practicals %}
  <li><a href="{{ practical.url | relative_url }}">{{ practical.title }}</a></li>
{% endfor %}
</ul> -->