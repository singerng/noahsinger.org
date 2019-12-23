---
title: Coursework
permalink: /courses
layout: default
---

# Coursework

{% for term in site.data.courses %}
<h3>{{ term.term }}</h3>

<div class="row ml-3 mb-3">
{% for course in term.courses %}
  <div class="col-md-6 col-sm-12">
	<h6>{% if course.code %}<em>{{ course.code }}:</em>{% endif %} {{ course.title }} {% if course.site %}<a href="{{ course.site }}" target="_blank"><i class="fas fa-external-link-alt"></i></a>{% endif %}</h6>
	{% if course.instructor %}<i class="fas fa-user"></i> {{ course.instructor }}{% endif %}
	{% if course.book %}<i class="fas fa-book"></i> <em>{{ course.book }}</em> ({{ course.author }}){% endif %}
	<p><small>{{ course.notes }}</small></p>
  </div>
{% endfor %}
</div>
{% endfor %}
