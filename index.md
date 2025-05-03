---
layout: home
title: Reflected Intelligence
---

<div class="home">
  <h1 class="page-heading">Reflected Intelligence</h1>

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
      {% if post.categories.size > 0 %}
      <div class="post-categories">
        <i class="fas fa-tags"></i>
        {% for category in post.categories %}
          <a href="{{ site.baseurl }}/categories/#{{ category | slugize }}" class="category-link">{{ category }}</a>{% unless forloop.last %}, {% endunless %}
        {% endfor %}
      </div>
      {% endif %}
      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
      <a href="{{ post.url | relative_url }}" class="read-more">Continue reading &raquo;</a>
    </div>
    {%- endfor -%}
  </div>

  <div class="about-section">
    <h2>About This Blog</h2>
    <p>Reflected Intelligence explores how AI systems mirror and reflect human intelligence. We pay close attention to the ways in which large language models and other AI technologies serve as cognitive mirrors that reveal as much about human cognition as they do about artificial intelligence.</p>
    <p><a href="/about/">Read more about this project &raquo;</a></p>
  </div>
</div>