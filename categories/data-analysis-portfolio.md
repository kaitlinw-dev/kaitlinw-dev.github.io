---
layout: archive
title: "Portfolio"
permalink: /portfolios/data-analysis/
# category: data-analysis-portfolio
# collection: data-analysis-portfolio
---

<a href="/portfolios/" class="back-to-portfolios">Back to All Portfolios</a>

{% include base_path %}

{% for post in site.data-analysis-portfolio %}
  {% include archive-single.html %}
{% endfor %}
