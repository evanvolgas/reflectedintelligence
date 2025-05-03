---
layout: page
title: Blog
permalink: /blog/
---

<div class="blog-archive">
  <div class="view-toggle">
    <button id="grid-view-btn" class="active"><i class="fas fa-th-large"></i> Grid</button>
    <button id="list-view-btn"><i class="fas fa-list"></i> List</button>
  </div>

  <ul class="post-list grid-layout" id="post-list">
    {%- for post in site.posts -%}
    <li class="post-item">
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      <span class="post-meta">
        {{ post.date | date: date_format }}

        {% assign words = post.content | strip_html | number_of_words %}
        {% assign reading_time = words | divided_by: 200 | plus: 1 %}
        <span class="reading-time"><i class="far fa-clock"></i> {{ reading_time }} min read</span>
      </span>

      <h3>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h3>

      {%- if post.categories.size > 0 -%}
      <span class="post-categories">
        <i class="fas fa-tags"></i>
        {% for category in post.categories limit:2 %}
          <a class="category-link" href="{{ site.baseurl }}/categories/#{{ category | slugize }}">{{ category }}</a>{% unless forloop.last %}, {% endunless %}
        {% endfor %}
        {% if post.categories.size > 2 %}...{% endif %}
      </span>
      {%- endif -%}

      <div class="post-excerpt">
        {{ post.excerpt }}
      </div>
      <a href="{{ post.url | relative_url }}" class="read-more">Continue reading <i class="fas fa-arrow-right"></i></a>
    </li>
    {%- endfor -%}
  </ul>
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const gridBtn = document.getElementById('grid-view-btn');
    const listBtn = document.getElementById('list-view-btn');
    const postList = document.getElementById('post-list');

    gridBtn.addEventListener('click', function() {
      postList.classList.add('grid-layout');
      postList.classList.remove('list-layout');
      gridBtn.classList.add('active');
      listBtn.classList.remove('active');
      localStorage.setItem('blogLayout', 'grid');
    });

    listBtn.addEventListener('click', function() {
      postList.classList.remove('grid-layout');
      postList.classList.add('list-layout');
      listBtn.classList.add('active');
      gridBtn.classList.remove('active');
      localStorage.setItem('blogLayout', 'list');
    });

    // Check saved preference
    const savedLayout = localStorage.getItem('blogLayout');
    if (savedLayout === 'list') {
      listBtn.click();
    }
  });
</script>

<style>
  .view-toggle {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1.5em;
  }

  .view-toggle button {
    background: none;
    border: 1px solid #ddd;
    padding: 0.5em 1em;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .view-toggle button:first-child {
    border-radius: 4px 0 0 4px;
  }

  .view-toggle button:last-child {
    border-radius: 0 4px 4px 0;
  }

  .view-toggle button.active {
    background-color: rgb(160, 222, 184);
    color: white;
    border-color: rgb(160, 222, 184);
  }

  .post-list.list-layout {
    display: block;
  }

  .post-list.list-layout .post-item {
    margin-bottom: 2em;
    padding-bottom: 2em;
    border-bottom: 1px solid #eee;
  }
</style>