---
title: Downloads
layout: page
---

For Visual Studio 2015 or later BI Developer Extensions can be installed from the Tools / Extensions and Updates menu.

{% for release in  site.github.releases %} 
- [{{ release.name }}]({{ release.assets[0].browser_download_url }})
   Downloads: {{ release.assets[0].download_count | intcomma }} | Size: {{ release.assets[0].size | filesize }} | Date: {{ release.assets[0].created_at | date_to_string}}
   
{% endfor %}

> Prior versions can be found on the old codeplex site at [http://bidshelper.codeplex.com](http://bidshelper.codeplex.com)