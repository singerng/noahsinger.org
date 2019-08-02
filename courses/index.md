---
title: Coursework
permalink: /courses
layout: default
---

# Coursework

{% for term in site.data.courses %}
<h3>{{ term.term }}</h3>

<div class="ml-3">
{% for course in term.courses %}
  <h6><em>{{ course.code }}:</em> {{ course.title }} {% if course.site %}<a href="{{ course.site }}" target="_blank"><i class="fas fa-external-link-alt"></i></a>{% endif %}</h6>
  <i class="fas fa-user"></i> {{ course.instructor }}
  <p><small>{{ course.content }}</small></p>
  <hr/>
{% endfor %}
</div>
{% endfor %}
