---
title: Show Extra Properties
category: ssas
component: ssasm
---

This feature exposes hidden properties on several Analysis Services objects. It also provides a better UI for editing descriptions on Analysis Services objects.

When this feature is on, the properties window for most Analysis Services objects changes. The Annotations property is exposed:

![](Show Extra Properties_AnnotationsTeaser.jpg)

Annotations can be used as custom properties on any Analysis Services object. For instance, if you would like to add a "PartitioningScheme" property to each measure group marking whether it should be partitioned by month or by year, you can do this with an annotation. Then custom AMO (Analysis Management Objects) code can inspect that annotation and build the appropriate partitions.

Also, this feature provides a better interface for entering multi-line descriptions:

![](Show Extra Properties_MultilineDescriptionPropertyTeaser.gif)

Finally, the FormatString and Description properties are made editable on linked measures. This shortcoming was reported [here](http://sqljunkies.com/WebLog/sqlbi/archive/2007/01/09/26685.aspx).

You can disable this feature with the Enabled Features dialog which can be found by choosing Tools... Options... then by choosing *{{site.title}}* on the left.