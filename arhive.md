---
layout: page
title: Arhive
subtitle: Zilele trec greu, anii trec uşor...
permalink: /arhive/
---

<section id="archive">
  {%for post in site.posts %}
    {% unless post.next %}
      <h3>{{ post.date | date: '%Y' }}</h3>
      <ul class="this">
    {% else %}
      {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
      {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
      {% if year != nyear %}
        </ul>
        <h3>{{ post.date | date: '%Y' }}</h3>
        <ul class="past">
      {% endif %}
    {% endunless %}
      <li><time>{{ post.date | date:"%d %b" }}</time> <a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
</section>
