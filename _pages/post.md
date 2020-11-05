---
permalink: /posts/
title: "Posts"
excerpt: "Minimal Mistakes is a flexible two-column Jekyll theme."
last_modified_at: 2020-11-02
---

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>