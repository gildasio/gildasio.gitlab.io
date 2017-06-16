---
layout: page
title: "Posts"
permalink: /posts/
---

Some text about somethings with more content than a [little post]({{ site.baseurl }}tips/).

<ul class="posts">
    {% for post in site.categories.posts %}
        <li>
            <a class="reserved" href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
