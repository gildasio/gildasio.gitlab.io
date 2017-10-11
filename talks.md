---
layout: page
title: "Talks"
permalink: /talks/
---

Uma lista com apresentações que eu fiz em alguns lugares.

<ul class="posts">
    {% for post in site.categories.talks %}
        <li>
            <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
            :
            <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
