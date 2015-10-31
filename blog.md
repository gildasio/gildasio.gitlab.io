---
layout: blog
title: "Posts"
permalink: /blog/
---

<ul class="posts">
    {% assign relevant = site.posts | except:"category","jekyll" %}
    {% for post in relevant %}
        <li>
            <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
            :
            <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
            @ {
            {% for category in post.categories %}<span><a href="{{ site.baseurl }}category/#{{ category }}" class="reserved">{{ category }}</a>{% if forloop.last != true %},{% endif %}</span>{% endfor %}
            }
        </li>
    {% endfor %}
</ul>
