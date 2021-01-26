---
title: Papers
permalink: /papers
layout: default
---

# Papers

### Research

<ul>
{% for paper in site.data.papers %}
{% if paper.type == "research" %}
{% include paper.html paper=paper %}
{% endif %}
{% endfor %}
</ul>

### Course Projects

<ul>
{% for paper in site.data.papers %}
{% if paper.type == "course_project" %}
{% include paper.html paper=paper %}
{% endif %}
{% endfor %}
</ul>

<!-- ### Expository -->
<!-- 
<ul>
{% for paper in site.data.papers %}
{% if paper.type == "expository" %}
  <li>
    <strong>{% if paper.paper %}
      <a href="/papers/{{ paper.paper }}" target="_blank" class="text-dark">{{ paper.title }}</a>.
    {% else %}
      {{ paper.title }}.
    {% endif %}</strong>{{ paper.authors }}. {{ paper.date |  date: "%B %Y" }}. <em>{{ paper.venue }}</em>.
  </li>
{% endif %}
{% endfor %}
</ul> -->

### Notes

<ul>
{% for paper in site.data.papers %}
{% if paper.type == "notes" %}
{% include paper.html paper=paper %}
{% endif %}
{% endfor %}
</ul>