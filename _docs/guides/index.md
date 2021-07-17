---
title: Guias
description: Guias sobre el uso de EVAB
index: True
---

# Guías

Guías para ejecutar Arena Brawl y programar tu bot!

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.docs %}
	{% if post.tags contains "guide" %}
	<div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>
	{% endif %}
	{% endfor %}
</div>
