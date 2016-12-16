---
title: Projects
permalink: /projects/
layout: default
---

## Projects

{% for project in site.data.projects %}
<div>
    <h3>{{ project.title }}</h3>

    By: {{ project.author }}
    <br/>

    {% if project.source %}
    <a href="{{ project.source }}" target="_blank">Source</a>
        {% if project.site %}
        | <a href="{{ project.site }}" target="_blank">Site</a>
        {% endif %}
    {% endif %}
    <br/>
    <div class="description">
        {{ project.description | markdownify }}
    </div>
</div>
{% endfor %}
