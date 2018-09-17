---
title: Coursework
permalink: /courses
layout: default
---

# Coursework

{% for term in site.data.courses %}
<h4>{{ term.term }}</h4>

{% for course in term.courses %}
  <h6><em>{{ course.code }}:</em> {{ course.title }}</h6>
  <i class="fas fa-user"></i> {{ course.instructor }} &mdash; <i class="fas fa-school"></i> {{ course.institution }}
  {% if course.site %}<a href="{{ course.site }}" target="_blank"><i class="fas fa-external-link-alt"></i></a>{% endif %}
  <p><small>{{ course.content }}</small></p>
  <hr/>
{% endfor %}
{% endfor %}
