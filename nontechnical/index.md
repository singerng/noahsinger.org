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
# Albums

<div class="row">
  {% for post in site.categories.albums %}
  <div class="col-lg-2 col-md-4 col-sm-6 text-center">
    <a href="{{ post.url }}">
      <img class="img-fluid" src="/static/images/albums/{{ post.album.image }}"/>
    </a>
    <h5 class="mt-2 mb-0"><em>{{ post.album.name }}</em></h5>
    {{ post.album.artist }} ({{ post.album.year }})
  </div>
  {% endfor %}
</div>

<br/><br/>
<sup>
  All album artwork on this website is taken from Wikipedia, in accordance
  with their <a href="https://en.wikipedia.org/wiki/Wikipedia:Non-free_content">
  standards for fair use</a> of copyrighted material. Images are low-resolution
  and contextually significant, since they uniquely identify and describe
  albums that are being written about. The details of the fair use rationale for any particular
  image can be viewed on its corresponding Wikipedia page.
</sup>
