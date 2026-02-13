{% assign akarsh_posts = site.posts | where_exp: "post", "post.categories contains 'Akarsh'" | sort: "date" | reverse %}

{% for post in akarsh_posts %}

[{{ post.title }}]({{ post.url | relative_url }})
{{ post.date | date: "%B %d, %Y" }}

{% endfor %}
