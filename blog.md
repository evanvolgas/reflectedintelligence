---
layout: page
title: Blog
permalink: /blog/
---

<div class="blog-archive">
  <ul class="post-list">
    {%- for post in site.posts -%}
    <li>
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      <span class="post-meta">{{ post.date | date: date_format }}</span>
      <h3>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h3>
      <p>
        {{ post.excerpt }}
      </p>
      <a href="{{ post.url | relative_url }}">Continue reading &raquo;</a>
    </li>
    {%- endfor -%}
  </ul>
</div>