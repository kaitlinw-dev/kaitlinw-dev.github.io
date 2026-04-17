---
layout: default
# title: "Articles"
permalink: /articles/
---

<h1 class="page__title">Articles</h1>
<p class="page__subtitle">Filter by topic or scroll to browse all posts.</p>

<div class="blog-category-container">

  <!-- MOBILE DROPDOWN -->
  <details class="blog-filter-dropdown">
    <summary class="btn">Filter Posts</summary>

    <div class="dropdown-content">
      <a href="/articles/" class="dropdown-item">All</a>

      <a href="/articles/cybersecurity/" class="dropdown-item">Cybersecurity</a>
      <a href="/articles/data-analysis/" class="dropdown-item">Data Analysis</a>

    </div>
  </details>

  <!-- DESKTOP BUTTONS -->
  <div class="blog-filter-buttons">

    <a href="/articles/cybersecurity/" class="blog-category-card">
      <h2>Cybersecurity</h2>
    </a>

    <a href="/articles/data-analysis/" class="blog-category-card">
      <h2>Data Analysis</h2>
    </a>

  </div>

</div>

<div class="blog-landing">
  {% include group-by-array collection=site.posts field="categories" %}

  {% for category in group_names %}
    {% assign posts = group_items[forloop.index0] %}
    <h2 id="{{ category | slugify }}" class="archive__subtitle">{{ category }}</h2>

    {% for post in posts %}
      {% include archive-single.html %}
    {% endfor %}
  {% endfor %}
</div>