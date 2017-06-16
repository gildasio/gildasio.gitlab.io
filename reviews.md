---
layout: blog
title: "Reviews"
permalink: /reviews/
---

<ul class="posts">
    {% for post in site.categories.reviews %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
