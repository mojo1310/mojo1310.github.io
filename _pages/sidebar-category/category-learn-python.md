---
title: "Programming: Python"
layout: archive
permalink: /learn/python
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['python']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
