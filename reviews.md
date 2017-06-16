---
layout: page
title: "Reviews"
permalink: /reviews/
---

Reviews about somethings like books, e-books, movies, tv shows ...

<ul class="posts">
    {% for post in site.categories.reviews %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
