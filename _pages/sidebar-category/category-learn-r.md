---
title: "Programming: R"
layout: archive
permalink: /learn/r
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['r']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
