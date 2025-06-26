---
title: "긴 글"
layout: archive
permalink: /art/writing_long
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['writing_long']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
