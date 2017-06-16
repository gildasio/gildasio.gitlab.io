---
layout: blog
title: "Tips & Tricks"
permalink: /tips/
---

Just a little posts, with no long explanation.

<ul class="posts">
    {% for post in site.categories.tips %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
