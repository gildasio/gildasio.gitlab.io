---
layout: page
title: "Tips & Tricks"
permalink: /tips/
---

Apenas pequenos posts, sem muitas explicações a respeito do assunto.

<ul class="posts">
    {% for post in site.categories.tips %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
