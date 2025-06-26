---
title: "발레"
layout: archive
permalink: /art/ballet
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['ballet']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
