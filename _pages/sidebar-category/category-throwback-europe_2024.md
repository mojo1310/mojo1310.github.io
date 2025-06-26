---
title: "2024 유럽 여행"
layout: archive
permalink: /throwback/europe_2024
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['europe_2024']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
