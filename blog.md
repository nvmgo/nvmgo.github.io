---
layout: default
---

{% for category in site.categories %}
{% if category[0] != 'product' %}
  <h2>{{ category[0] }}</h2>
  <ul class="posts">
    {% for post in category[1] %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endif %}
{% endfor %}