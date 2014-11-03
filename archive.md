---
title: Bob Gilmore - Archive
layout: default_layout
change_frequency: daily
priority: 1.0
---

<div id="archive">
  <h1>Archive</h1>
  <ul class="posts unstyled">
    {% for post in site.posts %}
      <li>
        {% include post_date_title.html %}
    </li>
    {% endfor %}
  </ul>
</div>
