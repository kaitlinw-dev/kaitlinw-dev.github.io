---
layout: archive
title: "Data Analysis Articles"
permalink: /articles/data-analysis/
category: data-analysis
---

<a href="/articles/" class="back-to-blog">Back to All Articles</a>

<div class="blog-post-list">

{% include base_path %}
{% for post in site.categories.data-analysis %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% include archive-single.html %}
{% endfor %}

</div>