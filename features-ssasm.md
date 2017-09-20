---
title: SSAS Multidimensional Features
layout: page
component: ssasm
---

The following are all the features that are applicable to Analysis Services (SSAS) Multidimensional projects

{% assign sorted_features = site.features | sort:  'title'  %}


{% for feature in sorted_features %}{% if feature.component contains page.component %} - [{{ feature.title }}]({{feature.url}}){% endif %}
{% endfor %}
