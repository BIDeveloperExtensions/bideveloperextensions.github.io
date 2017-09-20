---
layout: page
title: BI Developer Extensions
subtitle: The ultimate toolkit for Microsoft BI Developers
use-site-title: true
---
A Visual Studio add-in that enhances development functionality in Business Intelligence Development Studio (BIDS) and SQL Server Data Tools (SSDTBI).

_This project was previously called BIDS Helper (see [Project History](projecthistory))_

![](img/Home_BIDSHelperMontage.gif)

## Installation

Starting with *{{site.title}}* for SQL 2016 which is installed in Visual Studio 2015, install it from the [Visual Studio Gallery](/features/InstallingfromtheVisualStudioGallery).

To install *{{site.title}}* in earlier versions of Visual Studio, download the installer from the [downloads](/downloads) page. For silent installs you can run the setup .exe file with a /S command line option.

If for some reason you cannot use the installer the latest release includes an [xcopy deploy](/features/xcopydeploy) option.


## Documentation
All of the features in *{{site.title}}* are documented under the [Features](/features) menu.

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