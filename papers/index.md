---
title: Papers
permalink: /papers
layout: default
---

# Papers

Here I've collected papers that I've written for research projects and for pedagogy, etc.

### Research

{% for paper in site.data.papers %}
  {% if paper.type == "research" %}
  <div class="card mb-3">
    <div class="card-body">
      {% if paper.paper %}
        <a href="/papers/{{ paper.paper }}" target="_blank" class="text-dark"><h5 class="card-title">{{ paper.title }}</h5></a>
      {% else %}
        <h5 class="card-title">{{ paper.title }}</h5>
      {% endif %}
      
      <h6 class="card-subtitle mb-2 text-muted"><strong> {{ paper.authors }}</strong> &mdash; {{ paper.date |  date: "%B %Y" }} &mdash; <em>{{ paper.venue }}</em></h6>
    </div>
  </div>
  {% endif %}
{% endfor %}

### Education

{% for paper in site.data.papers %}
  {% if paper.type == "education" %}
  <div class="card mb-3">
    <div class="card-body">
      {% if paper.paper %}
        <a href="/papers/{{ paper.paper }}" target="_blank" class="text-dark"><h5 class="card-title">{{ paper.title }}</h5></a>
      {% else %}
        <h5 class="card-title">{{ paper.title }}</h5>
      {% endif %}
      
      <h6 class="card-subtitle mb-2 text-muted"><strong> {{ paper.authors }}</strong> &mdash; {{ paper.date |  date: "%B %Y" }} &mdash; <em>{{ paper.venue }}</em></h6>
    </div>
  </div>
  {% endif %}
{% endfor %}

