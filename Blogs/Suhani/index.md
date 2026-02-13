{% assign suhani_posts = site.posts | where_exp: "post", "post.categories contains 'Suhani'" | sort: "date" | reverse %}

{% for post in suhani_posts %}
### [{{ post.title }}]({{ post.url | relative_url }})

<small>{{ post.date | date: "%B %d, %Y" }}</small>

---

{% endfor %}
