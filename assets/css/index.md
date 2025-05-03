---
layout: default
---

<div class="home">
  <h1 class="page-heading">Reflected Intelligence</h1>

  <p class="page-subtitle">Exploring AI systems and how they reflect intelligence.</p>

  <div class="post-list">
    {%- for post in site.posts -%}
    <div class="post-item">
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      <span class="post-meta">{{ post.date | date: date_format }}</span>
      <h2>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h2>
      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
      <a href="{{ post.url | relative_url }}" class="read-more">Continue reading &raquo;</a>
    </div>
    {%- endfor -%}
  </div>
</div>