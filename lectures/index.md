---
title: Materials
permalink: /lectures
layout: default
---

# Materials

Here I've collected things like slides, notes, and papers that I've written for presentations, talks, and research projects. Feel free to contact me if
you notice errors in any of the materials. (I take no responsibility for inaccuracies in pre-2019 content.)

{% for lecture in site.data.lectures %}
  <div class="card mb-3">
    <div class="card-body">
      <h5 class="card-title">{{ lecture.title }}</h5>
      <h6 class="card-subtitle mb-2 text-muted"><strong>{{ lecture.date |  date: "%A, %B %d, %Y" }}</strong> &mdash; <strong>{{ lecture.venue }}</strong></h6>

      <p class="card-text">{{ lecture.description | markdownify }}</p>

      {% if lecture.slides %}
        <a href="/lectures/slides/{{ lecture.slides }}" target="_blank" class="btn btn-primary"><i class="fas fa-file-alt"></i> Slides</a>
      {% endif %}

      {% if lecture.paper %}
        <a href="/lectures/papers/{{ lecture.paper }}" target="_blank" class="btn btn-primary"><i class="fas fa-file-alt"></i> Paper/Notes</a>
      {% endif %}
    </div>
  </div>
{% endfor %}
