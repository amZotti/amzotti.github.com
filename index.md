---
layout: page
title: Under the Hood with Anthony Zotti
tagline: Coding made interesting
---
{% include JB/setup %}


<ul class="posts">
  {% for post in site.posts limit:1 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
    {{ post.content }}
    </li>
  {% endfor %}
</ul>
