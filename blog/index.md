---
title: singerng
permalink: /blog
layout: default
---

# Blog

I occasionally post on this blog for several reasons. Expository writing is helpful for me in solidifying my own understandings; I want to write down my activities for myself to remember in the future and for my family and friends to know what I'm up to; and if anyone is interested in CS or math and would benefit from the perspective of an undergraduate (probably unlikely), I am happy to offer it to them!

{% for post in site.posts %}
<div>
  <a href="{{ post.url }}" class="text-dark">
    <h3>{{ post.title | markdownify | remove: "<p>" | remove: "</p>" }}</h3>
  </a>

  <p class="text-muted">{{ post.date | date: "%B %d, %Y, %l:%M %p" }}</p>
  {{ post.excerpt | strip_html | truncatewords: 75 }}
  <br/><br/>

  {% assign tags = post.tags | sort %}
  {% for tag in tags %}
  	<a href="/tags#{{ tag }}" class="btn btn-info btn-sm mt-1"><i class="fas fa-tag"></i> {{ tag }}</a>
  {% endfor %}

  {% if forloop.last == false %}
    <hr/>
  {% endif %}
</div>
{% endfor %}
