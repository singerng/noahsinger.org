---
title: Papers
permalink: /papers
layout: default
---

The following papers are roughly organized (reverse) chronologically. You can also find my work on
<a href="https://dblp.org/pid/284/0977">DBLP</a> and
<a href="https://scholar.google.com/citations?hl=en&user=sJB6rcgAAAAJ">Google Scholar</a>. My <a href="https://orcid.org/0000-0002-0076-521X">ORCID</a>
is ``0000-0002-0076-521X``.

### Research papers

<ul class="paper-list">
{% for paper in site.data.papers %}
{% if paper.type == "research" %}
{% include paper.html paper=paper %}
{% endif %}
{% endfor %}
</ul>

### Other writings

<ul class="paper-list">
{% for paper in site.data.papers %}
{% if paper.type == "misc" %}
{% include paper.html paper=paper %}
{% endif %}
{% endfor %}
</ul>