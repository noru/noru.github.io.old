---
layout: page
title: test and a 
tagline: tagline
---

A First Level Header
====================

A Second Level Header
---------------------

Now is the time for all good men to come to
the aid of their country. This is just a
regular paragraph.

The quick brown fox jumped over the lazy
dog's back.

### Header 3

> This is a blockquote.
> 
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

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











