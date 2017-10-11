---
layout: page
title: "Posts"
permalink: /posts/
---

Alguns textos sobre algumas coisas, com mais conteúdo que [posts pequenos]({{ site.baseurl }}tips/).

<ul class="posts">
    {% for post in site.categories.posts %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
