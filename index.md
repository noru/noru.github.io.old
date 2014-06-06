---
layout: page
title: Hi Asshole!
tagline: have a nice day
---

<ul class="entries">
            {% for post in site.posts limit:1 %}
              <li>
                <a href="{{ post.url }}">
                <h3>{{ post.title }}</h3>
                <p class="blogdate">{{ post.date | date: "%d %B %Y" }}</p>
                <div>{{ post.content |truncatehtml | truncatewords: 60 }}</div>
                </a>
              </li>
            {% endfor %}
</ul>


<h1>All Posts<h1>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>












