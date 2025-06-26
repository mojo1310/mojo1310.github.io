---
title: "짧은 글"
layout: archive
permalink: /art/writing_short
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['writing_short']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
