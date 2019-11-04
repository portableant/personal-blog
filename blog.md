---
layout: default
permalink: /blog/
title: Erratic blogging
background: /images/layouts/kyoto.jpg
---

{% assign rows = site.posts.size | divided_by: 2.0 | ceil %}
{% for i in (1..rows) %}
  {% assign offset = forloop.index0 | times: 2 %}
  <div class="row">
  {% assign sorted = site.posts  %}
  {% for post in sorted limit:2 offset:offset %}
  <div class="col-md-6 mb-3">
    <div class="card card-body h-100
    intro-card ">

    <div class="container h-100">

      <!-- start image block -->
      {% if post.thumbnail %}
      <div class="cover-image ">
        <img class="align-self-center ml-1 mr-3 rounded-circle float-right thumb-post" src="{{ site.baseurl }}{{ post.thumbnail }}"
                     alt="{{page.title}}'s project image" height="150" width="150">
      </div>
      {% endif %}

      <!-- end image block -->

      <div class="contents-label mb-3">
      <h3>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </h3>
        <p>{{ post.date | date_to_string }}</p>
        {% if post.content != 'blank' %}
        <p class="card-text">
        {{ post.content | strip_html | truncatewords: 20}}
        </p>
        {% else %}
        <p>Just an image...</p>
        {% endif %}
      </div>
    </div>
    <a href="{{ site.baseurl }}{{ post.url }}" class="btn btn-primary mt-2">Read more</a>
  </div>

  </div>
  {% endfor %}
  </div>
  {% endfor %}
