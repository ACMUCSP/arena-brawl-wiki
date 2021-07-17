---
title: Instalacion
description: Como instalar EVAB de acuerdo a tu sistema operativo
index: True
---

# Instalación

Guías para instalar Arena Brawl de acuerdo al sistema operativo

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.docs %}
	{% if post.tags contains "installation" %}
	<div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>
	{% endif %}
	{% endfor %}
</div>
