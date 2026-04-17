---
layout: default
# title: "Portfolios"
permalink: /portfolios/
---

<h1 class="page__title">Portfolios</h1>
<p class="page__subtitle">Filter by topic or scroll to browse all projects.</p>

<div class="blog-category-container">

  <!-- MOBILE DROPDOWN -->
  <details class="blog-filter-dropdown">
    <summary class="btn">Filter Porfolios</summary>

    <div class="dropdown-content">
      <a href="/portfolios/" class="dropdown-item">All</a>

      <a href="/portfolios/cybersecurity/" class ="dropdown-item">Cybersecurity</a>
      <a href="/portfolios/data-analysis/" class="dropdown-item">Data Analysis</a>

    </div>
  </details>

  <!-- DESKTOP BUTTONS -->
  <div class="blog-filter-buttons">

    <a href="/portfolios/cybersecurity/" class ="portfolio-category-card">
    <h2>Cybersecurity</h2>
    <!-- <p>Cybersecurity projects.</p> -->
    </a>

    <a href="/portfolios/data-analysis/" class="portfolio-category-card">
    <h2>Data Analysis</h2>
    <!-- <p>Data analysis projects.</p> -->
    </a>

  </div>

</div>

<!-- <div class="article_landing">
<div class="article-top-row">


</div>

</div> -->

<div class="blog-landing">
{% include base_path %}


{% for post in site.portfolio %}
  {% include archive-single.html %}
{% endfor %}
</div>
