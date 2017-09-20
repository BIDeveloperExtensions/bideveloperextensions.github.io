---
title: News Archive
---

A chronological list of all news posts 

{% assign all_ann = site.posts | where: "index", false %}

<div class="posts"> 
  <ul>
  {% for ann in all_ann %}
  
    <li>
      <a href="{{ ann.url }}">
        {{ ann.date | date_to_string }} - {{ ann.title }}
      </a>
    </li>
  
  {% endfor %}
  </ul>
</div>