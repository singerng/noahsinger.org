---
title: Lectures
permalink: /lectures
layout: default
---

## Lectures

Here I've collected slides and papers/notes I've used for various presentations, talks,
lectures and tutorials throughout high school and beyond.

{% for lecture in site.data.lectures %}
  <div class="card mb-3">
    <div class="card-body">
      <h5 class="card-title">{{ lecture.title }}</h5>
      <h6 class="card-subtitle mb-2 text-muted"><strong>{{ lecture.date |  date: "%A, %B %d, %Y" }}</strong> for <strong>{{ lecture.venue }}</strong></h6>

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
