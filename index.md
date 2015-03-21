---
layout: page
title: Under the Hood with Anthony Zotti
tagline: Coding made interesting
---
{% include JB/setup %}


<ul class="posts">
  {% for post in site.posts %}

    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
    {{ post.content }}
    </li>
  {% endfor %}
</ul>
<a href="http://www.ontoplist.com/" target="_blank"><img src="http://www.ontoplist.com/images/ontoplist31.png?id=54a8a412f29ee" alt="Blog Directory & Business Pages - OnToplist.com" border="0" /></a>
<a href="http://globeofblogs.com" target="_blank"> <img
src="http://globeofblogs.com/buttons/globe_blogs.gif" alt="" width="80"
height="15"/></a>
<script type="text/javascript" src="http://counter5.allfreecounter.com/private/counter.js?c=9c753a83be5fd40f894be6e4d5b3ccce"></script>
