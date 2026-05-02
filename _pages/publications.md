---
layout: single
title: Publications
permalink: /publications/
author_profile: true
---

<style>
  .controls {
    padding: 1rem;
    background: #f2f3f3;
    margin-bottom: 2rem;
    border-radius: 4px;
  }
  .control {
    position: relative;
    display: inline-block;
    padding: 0.5rem 1rem;
    background: #fff;
    color: #494e52;
    cursor: pointer;
    font-size: 0.8rem;
    margin-right: 0.5rem;
    margin-bottom: 0.5rem;
    border: 1px solid #e2e2e2;
    border-radius: 4px;
    transition: background 150ms;
  }
  .control:hover {
    background: #e2e2e2;
  }
  .control-active {
    background: #6f777d;
    color: #fff;
  }
  .publication-item {
    display: inline-block;
    width: 100%;
    margin-bottom: 1.5rem;
    padding: 1rem;
    border-bottom: 1px solid #f2f3f3;
    transition: transform 0.2s;
  }
  .publication-item:hover {
    transform: translateX(10px);
  }
  .publication-title {
    font-weight: bold;
    font-size: 1.1rem;
    display: block;
  }
  .publication-meta {
    font-size: 0.9rem;
    color: #6f777d;
  }
  .tag {
    display: inline-block;
    padding: 0.2rem 0.5rem;
    background: #e2e2e2;
    font-size: 0.7rem;
    border-radius: 3px;
    margin-right: 0.3rem;
  }
</style>

<div class="controls">
  <strong>Filter by Field:</strong><br>
  <button type="button" class="control" data-filter="all">All</button>
  {% assign fields = site.data.publications | map: "field" | uniq | sort %}
  {% for field in fields %}
    <button type="button" class="control" data-filter=".{{ field | slugify }}">{{ field }}</button>
  {% endfor %}
  <br>
  <strong>Filter by Theme:</strong><br>
  {% assign themes = site.data.publications | map: "theme" | uniq | sort %}
  {% for theme in themes %}
    <button type="button" class="control" data-filter=".{{ theme | slugify }}">{{ theme }}</button>
  {% endfor %}
  <br>
  <strong>Sort by Year:</strong><br>
  <button type="button" class="control" data-sort="year:asc">Oldest First</button>
  <button type="button" class="control" data-sort="year:desc">Newest First</button>
</div>

<div id="publications-container" class="publications-list">
  {% assign sorted_pubs = site.data.publications | sort: "year" | reverse %}
  {% for pub in sorted_pubs %}
    <div class="mix publication-item {{ pub.field | slugify }} {{ pub.theme | slugify }}" data-year="{{ pub.year }}">
      <a href="{{ pub.url }}" class="publication-title">{{ pub.title }}</a>
      <div class="publication-meta">
        {{ pub.authors }} ({{ pub.year }}). <em>{{ pub.journal }}</em>
      </div>
      <div class="publication-tags">
        <span class="tag">{{ pub.field }}</span>
        <span class="tag">{{ pub.theme }}</span>
      </div>
    </div>
  {% endfor %}
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/mixitup/3.3.1/mixitup.min.js"></script>
<script>
  var containerEl = document.querySelector('#publications-container');
  var mixer = mixitup(containerEl, {
    selectors: {
      target: '.mix'
    },
    animation: {
      duration: 300
    }
  });
</script>
