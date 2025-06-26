---
title: "2013 산티아고순례길"
layout: archive
permalink: /throwback/santiago_2013
author_profile: true
sidebar:
  nav: "sidebar-category"
types: posts
---

{% assign posts = site.categories['santiago_2013']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
