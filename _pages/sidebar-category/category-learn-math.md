---
title: "수학"
layout: archive
permalink: /learn/math
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['math']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
