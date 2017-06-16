---
layout: blog
title: "Posts"
permalink: /posts/
---

<ul class="posts">
    {% for post in site.categories.posts %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
