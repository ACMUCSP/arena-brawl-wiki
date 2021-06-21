---
layout: page
title: Documentation
permalink: /docs/
---

# Documentacion

Bienvenidos a la documentacion de {{ site.title }}! Aqui encontraras las secciones:

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.docs %}
    <div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>{% endfor %}
</div>
