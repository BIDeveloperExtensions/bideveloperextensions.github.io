---
title: Common Features
layout: page
component: common
---

The following are all the features that are common across the various BI projects types

{% assign sorted_features = site.features | sort:  'title'  %}

{% for feature in sorted_features %}{% if feature.component contains page.component %} - [{{ feature.title }}]({{feature.url}}){% endif %}
{% endfor %}
