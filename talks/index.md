---
title: Talks
permalink: /talks
layout: default
---

# Talks

I've given a number of talks and presentations, and have linked here the slides. Feel free to contact me if
you notice errors in any of the materials.

{% for talk in site.data.talks %}
  <div class="card mb-3">
    <div class="card-body">
      <a href="/talks/{{ talk.slides }}" target="_blank" class="text-dark"><h5 class="card-title">{{ talk.title }}</h5></a>
      <h6 class="card-subtitle mb-2 text-muted"><strong> {{ talk.authors }}</strong> &mdash; {{ talk.date |  date: "%A, %B %d, %Y" }} &mdash; <em>{{ talk.venue }}</em></h6>
    </div>
  </div>
{% endfor %}
