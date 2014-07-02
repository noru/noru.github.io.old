---
layout: page
title: Hi Asshole!
tagline: I Wish You Hurt Yourself While You Sleep
---
<link rel="shortcut icon" type="image/x-icon" href="http://docsteach.org/images/youtube-icon-16x16.png">

<ul class="entries">
            {% for post in site.posts limit:1 %}
              <li>
                <a href="{{ post.url }}">
                <h2>{{ post.title }}</h2>
                <p class="blogdate">{{ post.date | date: "%d %B %Y" }}</p>
                <div>{{ post.content }}</div>
                </a>
              </li>
            {% endfor %}
</ul>

<br>
<h2>All Posts</h2>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
<br>
<br>











