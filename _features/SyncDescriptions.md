---
title: Sync Descriptions
category: ssas
component: ssasm
---
In a SQL Server relational database, you can add descriptions to tables and columns using extended properties. Commonly, the {"MS_Description"} extended property is used, but other extended properties can be used. If you have spent considerable time entering descriptions for relational tables and columns (for example, using the [Kimball Dimensional Modeling Spreadsheet](http://www.kimballgroup.com/html/booksMDWTtools.html)), *{{site.title}}* Sync Descriptions can help you import those descriptions to the dimension in Analysis Services.

Select one or more dimensions then right click and choose Sync Descriptions...

![](Sync Descriptions_SyncDescriptionsMenu.png)

Then a window pops up showing you all the extended properties in the relational database. Choose the extended property used as the description. Then choose any additional columns that you would like to show in the dimension attributes.

![](Sync Descriptions_SyncDescriptionsPopup.png)

Let's say you have a column with the {"MS_Description"} property set to "The geographic region of the country" and the "Example Values" property set to "North, East, South, West". The description property for the corresponding attribute in Analysis Services will be set to:

_The geographic region of the country_
_Example Values: North, East, South, West_

Descriptions are applied to the dimension itself and to attributes within that dimension. Descriptions will be applied to any attribute with a NameColumn or with only one KeyColumn.

This Sync Descriptions feature works for Multidimensional models. For the equivalent feature in Tabular models, see [Tabular Sync Descriptions](../TabularSyncDescriptions) which leverages the same code.

Limitations:

* Your dimension must be tied to a table or view in the DSV, not to a named query in the DSV.
* Only SQL Server relational databases are supported.
* Currently, the sync only works in one direction. You can only sync relational database descriptions into Analysis Services.
* Currently, Sync Descriptions only operates on Analysis Services dimensions, not measure groups.

