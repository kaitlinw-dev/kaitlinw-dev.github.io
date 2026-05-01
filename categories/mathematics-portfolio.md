---
layout: archive
title: "Mathematics Portfolio"
permalink: /portfolios/mathematics/
# category: mathematics-portfolio
tags: [mathematics-portfolio]
---

<a href="/portfolios/" class="back-to-portfolios">Back to All Portfolios</a>


<div class="blog-post-list">
{% include base_path %}

{% for post in site.portfolio %}
  {% if post.tags and post.tags contains "mathematics-portfolio" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}
</div>