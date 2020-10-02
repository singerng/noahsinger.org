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
  <li>
    <strong>{% if paper.paper %}
      <a href="/papers/{{ paper.paper }}" target="_blank" class="text-dark">{{ paper.title }}</a>.
    {% else %}
      {{ paper.title }}.
    {% endif %}</strong>

    {{ paper.authors }}. {{ paper.date |  date: "%B %Y" }}. <em>{{ paper.venue }}</em>.
  </li>
{% endif %}
{% endfor %}
</ul>

<!-- ### Expository -->

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
</ul>

### Notes

<ul>
{% for paper in site.data.papers %}
{% if paper.type == "notes" %}
  <li>
    <strong>{% if paper.paper %}
      <a href="/papers/{{ paper.paper }}" target="_blank" class="text-dark">{{ paper.title }}</a>.
    {% else %}
      {{ paper.title }}.
    {% endif %}</strong>{{ paper.authors }}. {{ paper.date |  date: "%B %Y" }}. <em>{{ paper.venue }}{% if paper.scribing %}. Scribing {{ paper.scribing }}{% endif %}</em>.
  </li>
{% endif %}
{% endfor %}
</ul>