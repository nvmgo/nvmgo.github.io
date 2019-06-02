---
layout: default
---
  
{% for category in site.categories %}
{% if category[0] == 'product' %}
{% for post in category[1] %}
<div id="post">
    <h1 id="{{post.title}}">{{post.title}}</h1>
    <p>{{ post.excerpt }}</p>
    <p><a href="{{ BASE_PATH }}{{ post.url }}">more</a></p>
</div>
{% endfor %}
{% endif %}
{% endfor %}