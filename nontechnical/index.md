---
title: Non-Technical
permalink: /nontech
layout: default
---

# Non-Technical

You can tell a lot about a person by what they watch, read, and listen to. To that
end, I'm using my blog to compile my thoughts about the albums, films, shows,
and books that have been the most meaningful for or influential on me. Some are
extremely popular today, others are practically unknown, whether due to age
or low mass appeal. Each of these articles
are written in "review" format, but I'm not meaning to review the merits of the works
as much as review their influence on me and the people I'm close to. Hopefully, I'll
get some more people interested in them as well!


<a id="albums"/>

<div class="card mb-4">
  <div class="card-header">
    <h3 class="card-title"><i class="fas fa-headphones"></i> Albums</h3>
  </div>
  <div class="card-body">
  {% for post in site.categories.albums %}
    <a href="{{ post.url }}" class="text-dark">
      <h4>{{ post.title | markdownify | remove: "<p>" | remove: "</p>" }}</h4>
    </a>
    <h5><em>{{ post.album.name }}</em> by {{ post.album.artist }} ({{ post.album.year }})</h5>
    <p class="text-muted">{{ post.date | date: "%B %d, %Y, %l:%M %p" }}</p>
  {% endfor %}
  </div>
</div>
