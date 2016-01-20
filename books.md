---
layout: blog
title: "Books Review"
permalink: /books/
---

<ul class="posts">
    {% for post in site.categories.books %}
        <li>
            <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
            :
            <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
