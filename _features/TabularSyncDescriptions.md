---
title: Tabular Sync Descriptions
category: ssas
component: ssast
compatibilitylevel:  
    - 1103
    - 1200
    - 1400
---

In a SQL Server relational database, you can add descriptions to tables and columns using extended properties. Commonly, the {"MS_Description"} extended property is used, but other extended properties can be used. If you have spent considerable time entering descriptions for relational tables and columns (for example, using the [Kimball Dimensional Modeling Spreadsheet](http://www.kimballgroup.com/html/booksMDWTtools.html)), *{{site.title}}* Tabular Sync Descriptions can help you import those descriptions to the table in your Tabular model in Analysis Services.

In the diagram view, right click on the name of a table and choose Sync Descriptions...

![](Tabular Sync Descriptions_TabularSyncDescriptionsMenu.png)

Then a window pops up showing you all the extended properties in the relational database. Choose the extended property used as the description. Then choose any additional columns that you would like to show in the description.

![](Tabular Sync Descriptions_SyncDescriptionsPopup.png)

Let's say you have a column with the {"MS_Description"} property set to "The geographic region of the country" and the "Example Values" property set to "North, East, South, West". The description property for the corresponding column in the table in Analysis Services will be set to:

_The geographic region of the country_
_Example Values: North, East, South, West_

Descriptions are applied to the table itself and to columns within that table. Descriptions are only applied to regular columns, not calculated columns or measures.

Considering that the Description property appears in a tooltip in the Power View field list, setting descriptions is a key to building a self-documenting model which is easy for business users to use for ad-hoc reporting:

![](Tabular Sync Descriptions_TabularSyncDescriptionsPowerViewFieldList.png)

This feature leverages the same code as the [Sync Descriptions](../SyncDescriptions) feature for Multidimensional models.

Limitations:

* Only SQL Server relational databases are supported.
* Currently, the sync only works in one direction. You can only sync relational database descriptions into Analysis Services.
* Currently, Sync Descriptions only operates on Analysis Services tables in a Tabular model, not calculated columns or measures.

