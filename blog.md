---
layout: default
title: "Blog"
description: "Insights on Cloud, DevOps, AIOps, and Enterprise Release Engineering"
permalink: /blog/
---
<h1>Blog</h1>
<p>Thoughts, tutorials, and insights from my work in Cloud, DevOps, AI, and Enterprise Release Engineering.</p>

{% assign posts = site.posts %}
<ul style="list-style:none; padding-left:0;">
  {% for post in posts %}
  <li style="margin:18px 0;">
    <a href="{{ post.url | relative_url }}" style="font-weight:600;">{{ post.title }}</a>
    <div><small>{{ post.date | date: "%b %-d, %Y" }}</small></div>
    {% if post.description %}
      <div><small>{{ post.description }}</small></div>
    {% endif %}
  </li>
  {% endfor %}
</ul>
