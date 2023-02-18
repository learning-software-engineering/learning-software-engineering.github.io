---
layout: page
title: assignment
permalink: /assg3
nav: true
---


{% assign orderedlist = site.assg3 %}
{% for entry in orderedlist %}
  <p>
    <a href="{{site.baseurl}}{{entry.url}}">
      {{ entry.title }}
    </a>
  </p>
{% endfor %}
