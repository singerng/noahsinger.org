---
title: Papers
permalink: /papers
layout: default
---

The following papers are roughly organized (reverse) chronologically. You can also find my work on
[DBLP](https://dblp.org/pid/284/0977) and [Google Scholar](https://scholar.google.com/citations?hl=en&user=sJB6rcgAAAAJ). My ORCID is [``0000-0002-0076-521X``](https://orcid.org/0000-0002-0076-521X). See also this [YouTube playlist](https://youtube.com/playlist?list=PLUhFhv9En0UGP13PyAsYwNmq0_xfgZaUX) of my research talks.

{% if site.data.papers.manuscripts.size != 0 %}

### Technical manuscripts

<ul class="paper-list">
{% for paper in site.data.papers.manuscripts %}
{% include paper.html paper=paper %}
{% endfor %}
</ul>

{% endif %}

### Technical publications

<ul class="paper-list">
{% for paper in site.data.papers.publications %}
{% include paper.html paper=paper %}
{% endfor %}
</ul>

### Miscellaneous writing

<ul class="paper-list">
{% for paper in site.data.papers.misc %}
{% include paper.html paper=paper %}
{% endfor %}
</ul>