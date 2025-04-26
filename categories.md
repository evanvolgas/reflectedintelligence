---
layout: page
title: Categories
permalink: /categories/
---

<div class="categories-page">
  <p>Browse all articles by category:</p>

  {% assign sorted_categories = site.categories | sort %}
  
  <div class="category-list">
    {% for category in sorted_categories %}
      <a href="#{{ category[0] | slugize }}" class="category-badge">{{ category[0] }} ({{ category[1].size }})</a>
    {% endfor %}
  </div>

  <div class="category-sections">
    {% for category in sorted_categories %}
    <div class="category-section" id="{{ category[0] | slugize }}">
      <h2>{{ category[0] }}</h2>
      <ul class="post-list">
        {% assign sorted_posts = category[1] | sort: 'date' | reverse %}
        {% for post in sorted_posts %}
          <li>
            <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
            <h3>
              <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
            </h3>
            {% if post.description %}
              <p class="post-description">{{ post.description }}</p>
            {% endif %}
          </li>
        {% endfor %}
      </ul>
      <a href="#" class="back-to-top">Back to top ↑</a>
    </div>
    {% endfor %}
  </div>
</div>

<style>
  .category-list {
    margin: 2em 0;
  }
  
  .category-badge {
    display: inline-block;
    background-color: #f0f0f0;
    padding: 0.3em 0.8em;
    margin: 0.3em 0.2em;
    border-radius: 3px;
    font-size: 0.9em;
    text-decoration: none;
    color: #333;
    transition: background-color 0.2s;
  }
  
  .category-badge:hover {
    background-color: #e0e0e0;
    text-decoration: none;
  }
  
  .category-section {
    margin-bottom: 3em;
    padding-top: 1em;
    border-top: 1px solid #eee;
  }
  
  .post-description {
    color: #666;
    font-size: 0.9em;
    margin-top: 0.5em;
  }
  
  .back-to-top {
    display: inline-block;
    margin-top: 1em;
    font-size: 0.9em;
  }
  
  .post-list {
    list-style: none;
    padding-left: 0;
  }
  
  .post-list li {
    margin-bottom: 1.5em;
  }
  
  .post-list h3 {
    margin-top: 0.3em;
    margin-bottom: 0.3em;
  }
</style>
