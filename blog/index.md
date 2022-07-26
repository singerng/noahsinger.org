---
title: Blog (singerng)
permalink: /blog
layout: default
---

# Blog

{% for post in site.posts %}
<div>
  <a href="{{ post.url }}" class="text-dark">
    <h3>{{ post.title | markdownify | remove: "<p>" | remove: "</p>" }}</h3>
  </a>

  <p class="text-muted">{{ post.date | date: "%B %d, %Y" }}</p>
  {{ post.excerpt | strip_html | truncatewords: 75 }}
  <br/><br/>

  {% assign tags = post.tags | sort %}
  {% include taglist.html tags=tags %}

  {% if forloop.last == false %}
    <hr/>
  {% endif %}
</div>
{% endfor %}
