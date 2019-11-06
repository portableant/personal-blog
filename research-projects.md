---
layout: default
category: research
title: Projects
background: '/images/layouts/fushimi.jpg'
---

This page documents various projects I've worked on over my career in museums.
Some of these are more richly documented than others, but I try to include links
to code, publications and funding details where possible.

{% assign rows = site.projects.size | divided_by: 2.0 | ceil %}
{% for i in (1..rows) %}
  {% assign offset = forloop.index0 | times: 2 %}
  <div class="row">
  {% assign sorted = site.projects | sort:"title" %}
  {% for author in sorted limit:2 offset:offset %}
  <div class="col-md-6 mb-3">

    <div class="card card-body h-100 intro-card ">
  <div class="container head" style="max-height:100;"></div>
    <div class="container h-100">

      <!-- start image block -->

      <div class="cover-image ">
        <img class="align-self-center ml-1 mr-3 rounded-circle float-right thumb-post" src="{{ site.baseurl }}/images/projects/{{ author.thumbnail }}"
                     alt="{{page.title}}'s project image" height="150" width="150">
      </div>

      <!-- end image block -->

      <div class="contents-label mb-3">
      <h3>
        <a href="{{ site.baseurl }}{{ author.url }}">{{ author.title }}</a>
      </h3>
        <p class="card-text">{{ author.content | strip_html | truncatewords: 20}}</p>
      </div>
    </div>
    <a href="{{ site.baseurl }}{{ author.url }}" class="btn btn-primary mt-2">Read more</a>
  </div>

  </div>
  {% endfor %}
  </div>
  {% endfor %}
