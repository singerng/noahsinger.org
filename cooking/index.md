---
title: Cooking
permalink: /cooking
layout: default
---

### Cooking

Baking and cooking are some of my favorite hobbies; this page has some of my favorite photos of my bakes and dishes from the past several years. I draw primarily from
<a href="https://www.cooksillustrated.com">Cook's Illustrated</a> (including
their wonderful <em>Baking Book</em>) as well as
<a href="https://cooking.nytimes.com">New York Times Cooking</a>.

#### Sweets (and other baking)

<div class="container">
	<div class="row">
{% for item in site.data.cooking %}
{% if item.type == "sweet" %}
		<div class="col-sm-3">
			<div class="card mb-3">
	            <img src="/cooking/{{ item.photo }}" class="card-img-top"/>
	            <div class="card-body p-2">
	            	<p class="small-card-h"><strong>{{ item.title }}</strong>
	            	{% if item.source %}<span class="text-muted">from {{ item.source }}</span>{% endif %}</p>
	            </div>
	        </div>
	    </div>
{% endif %}
{% endfor %}
	</div>
</div>

<br/>

#### Savory stuff

<div class="container">
	<div class="row">
{% for item in site.data.cooking %}
{% if item.type == "savory" %}
		<div class="col-sm-3">
			<div class="card mb-3">
	            <img src="/cooking/{{ item.photo }}" class="card-img-top"/>
	            <div class="card-body p-2">
	            	<p class="small-card-h"><strong>{{ item.title }}</strong>
	            	{% if item.source %}<span class="text-muted">from {{ item.source }}</span>{% endif %}</p>
	            </div>
	        </div>
	    </div>
{% endif %}
{% endfor %}
	</div>
</div>