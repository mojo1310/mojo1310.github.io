---
title: "디지털 전환 프로젝트 회고"
layout: archive
permalink: /learn/project
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['project']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
