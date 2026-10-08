---
permalink: /
title: "Tianxiang's Homepage"
excerpt: ""
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

{% include_relative includes/intro.md %}

{% include_relative includes/exp.md %}

{% include_relative includes/open_source.md %}

{% include_relative includes/pub.md %}

{% include_relative includes/role.md %}
