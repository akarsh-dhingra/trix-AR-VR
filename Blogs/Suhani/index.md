---
layout: page
title: Suhani's Blog Series
---

# Suhani's AR-VR Blog Collection

{% assign suhani_posts = site.posts | where_exp: "post", "post.categories contains 'Suhani'" %}

{% for post in suhani_posts %}
  ## [{{ post.title }}]({{ post.url }})
  <small>{{ post.date | date: "%B %d, %Y" }}</small>

  {{ post.excerpt }}

  ---
{% endfor %}
