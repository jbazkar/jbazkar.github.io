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
<!-- Post header banner -->
<section class="post-hero">
  <h1>{{ page.title }}</h1>
  <p class="post-meta">Published on {{ page.date | date: "%B %d, %Y" }}</p>

  <!-- 👁 Per-post page views -->
  <div style="margin-top:8px; font-size:14px; color:#a8b0c3;">
    <span id="post-views" data-page="{{ page.url | escape }}"
          style="display:inline-flex; align-items:center; gap:6px;">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none"
           stroke="var(--accent, #66d9e8)" stroke-width="2"
           stroke-linecap="round" stroke-linejoin="round">
        <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
        <circle cx="12" cy="12" r="3"/>
      </svg>
      Page views: …
    </span>
  </div>
  <!-- end views -->
</section>

<!-- Main post content -->
<article class="post-body">
  {{ content }}
</article>

<!-- Author box -->
<section class="author-box">
  <img class="author-avatar" src="{{ page.author.avatar | default: site.author.avatar }}" alt="{{ page.author.name | default: site.author.name }}">
  <div class="author-meta">
    <h3 class="author-name">{{ page.author.name | default: site.author.name }}</h3>
    <p class="author-title">{{ page.author.title | default: site.author.title }}</p>
    {% assign links = page.author.links | default: site.author.links %}
    {% if links %}
      <p class="author-links">
        {% for l in links %}
          <a href="{{ l.url }}" target="_blank" rel="noopener">{{ l.text }}</a>{% unless forloop.last %} · {% endunless %}
        {% endfor %}
      </p>
    {% endif %}
  </div>
</section>

<!-- Post footer navigation -->
<hr>
<nav class="post-nav">
  <div class="post-prev">
    {% if page.previous %}
      ← <a href="{{ page.previous.url | relative_url }}">{{ page.previous.title }}</a>
    {% endif %}
  </div>
  <div class="post-next">
    {% if page.next %}
      <a href="{{ page.next.url | relative_url }}">{{ page.next.title }}</a> →
    {% endif %}
  </div>
</nav>

<!-- 🔁 Views script (uses Lambda + DynamoDB) -->
<script>
  (function () {
    const el = document.getElementById("post-views");
    if (!el) return;

    // Use Jekyll page.url as the unique key, e.g. /blog/my-post/
    const pageKey = el.getAttribute("data-page") || "/blog/unknown";

    // Your existing API Gateway URL
    const endpointBase = "https://jmgf0i5809.execute-api.us-east-1.amazonaws.com/prod/views";
    const endpoint = endpointBase + "?page=" + encodeURIComponent(pageKey);

    fetch(endpoint)
      .then(res => res.json())
      .then(data => {
        console.log("Post views API:", data);
        if (typeof data.views === "number") {
          el.innerHTML = `
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none"
                 stroke="var(--accent, #66d9e8)" stroke-width="2"
                 stroke-linecap="round" stroke-linejoin="round">
              <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
              <circle cx="12" cy="12" r="3"/>
            </svg>
            Page views: ${data.views}
          `;
        } else {
          el.textContent = "Page views: 0";
        }
      })
      .catch(err => {
        console.error("Post view counter error:", err);
        el.textContent = "Page views: 0";
      });
  })();
</script>
W
