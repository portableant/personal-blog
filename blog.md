---
layout: default
permalink: /blog/
title: Erratic blogging
background: /images/layouts/kyoto.jpg
---
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
