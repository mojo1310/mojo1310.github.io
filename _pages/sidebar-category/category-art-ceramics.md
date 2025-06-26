---
title: "도예"
layout: archive
permalink: /art/ceramics
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['ceramics']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
