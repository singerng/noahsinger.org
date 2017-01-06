---
title: Lectures
permalink: /lectures/
layout: default
---

## Lectures

{% for lecture in site.data.lectures %}
<div>
    <h3>{{ lecture.title }}</h3>

    {{ lecture.date |  date: "%A, %B %d, %Y" }} at {{ lecture.venue }}

    <br/>

    <div class="description">
        {{ lecture.description | markdownify }}
    </div>

    <a href="/lectures/slides/{{ lecture.slides }}" target="_blank">Slides</a>
        {% if lecture.notes %}
        | <a href="/lectures/notes/{{ lecture.notes }}" target="_blank">Notes</a>
        {% endif %}
    <br/>
</div>
{% endfor %}
