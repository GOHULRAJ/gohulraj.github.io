
---
layout: archive
title: Blog Posts
permalink: /blog/
---

{% for post in site.posts %}
  <article class="archive-item">
    <h4><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h4>
    <small>{{ post.date | date: "%B %d, %Y" }} • {{ post.categories | join: ', ' }}</small>
  </article>
{% endfor %}
