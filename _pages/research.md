---
layout: single
title: Research
permalink: /research/
author_profile: true
---

Information about my current research will go here.

### Recent Updates
<ul>
  {% for update in site.updates %}
    <li><a href="{{ update.url }}">{{ update.date | date: "%B %d, %Y" }} - {{ update.title }}</a></li>
  {% endfor %}
</ul>
