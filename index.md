---
layout: page
title: BI Developer Extensions
subtitle: The ultimate toolkit for Microsoft BI Developers
use-site-title: true
---
A Visual Studio extension that enhances development functionality in Business Intelligence Development Studio (BIDS) and SQL Server Data Tools (SSDT).

_This project was previously called BIDS Helper (see [Project History](projecthistory))_

![](img/Home_BIDSHelperMontage.gif)

## Installation

Starting with Visual Studio 2015, {{site.title}} is installed from the [Visual Studio Marketplace](/downloads/).

For install instructions with earlier versions of Visual Studio, see the [downloads](/downloads/) page.


## Documentation
All of the features in *{{site.title}}* are documented under the *Features* menu.

{% assign sorted_features = site.features | sort:  'title'  %}

{% for comp in site.data.components %}
#### {{comp.title}} Features
{% for feature in sorted_features %}{% if feature.component contains comp.name or feature.category contains comp.name %} - [{{ feature.title }}]({{feature.url}}){% endif %}
{% endfor %}
{% endfor %}


## News

{% assign recent = site.posts | where: "index", "false"  %}
<div class="posts"> 
  <ul>
  {% for ann in recent limit: 3 %}
  
    <li>
      <a href="{{ ann.url }}">
        {{ ann.date | date_to_string }} - {{ ann.title }}
      </a>
    </li>
  
  {% endfor %}
  </ul>
</div>

<div>
  <div >
    <a class="btn btn-default" href="/news">See all past news</a>
  </div>
</div>