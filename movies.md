---
layout: blog
title: "Movies Review"
permalink: /movies/
---

<ul class="posts">
    {% for post in site.categories.movies %}
        <li>
            <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
            :
            <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
