---
layout: default
title: "Blog – AI, Cloud & DevOps Insights by Baskaran Jeyarajan"
description: "Articles and research notes on Cloud, DevOps, AIOps, and Enterprise Release Engineering — covering real-world frameworks like SmartOps and predictive automation in platform delivery."
permalink: /blog/
image: "/assets/img/blog-banner.png"
---


<!-- Blog hero banner -->
<section class="blog-hero">
  <h1>My Blog & Insights</h1>
  <p>Exploring Cloud, DevOps, AIOps, and Enterprise Release Leadership — one story at a time.</p>
</section>

<!-- Blog post listing -->
<section class="blog-list">
  {% assign posts = site.posts %}
  <ul style="list-style:none; padding-left:0;">
    {% for post in posts %}
    <li style="margin:24px 0; border-bottom:1px solid #e0e0e0; padding-bottom:12px;">
      <a href="{{ post.url | relative_url }}" class="blog-link">{{ post.title }}</a>
      <div><small>{{ post.date | date: "%b %-d, %Y" }}</small></div>
      {% if post.description %}
        <div><small>{{ post.description }}</small></div>
      {% endif %}
    </li>
    {% endfor %}
  </ul>
</section>
