---
layout: page
title: "Reviews"
permalink: /reviews/
---

Reviews sobre coisas como livros, e-books, filmes, documentários, séries ...

<ul class="posts">
    {% for post in site.categories.reviews %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
