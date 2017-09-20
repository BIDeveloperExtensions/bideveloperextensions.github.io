---
title: SSRS Features
layout: page
component: ssrs
---

The following are all the features that are applicable to Reporting Services (SSRS) projects

{% assign sorted_features = site.features | sort:  'title'  %}

{% for feature in sorted_features %}{% if feature.component contains page.component %} - [{{ feature.title }}]({{feature.url}}){% endif %}
{% endfor %}
