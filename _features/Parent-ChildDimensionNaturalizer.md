---
title: Parent-Child Dimension Naturalizer
category: ssas
component: ssasm
---

_Note: This feature integrates the code from the [Parent-Child Dimension Naturalizer project](http://www.codeplex.com/PCDimNaturalize) into {{site.ms-designer}}. Special thanks go to Jon Burchel for permission to use that code._

The Parent-Child Dimension Naturalizer aids in converting parent-child dimensions into natural hierarchies. Natural hierarchies perform better primarily because aggregations can be built up a natural hierarchy, while aggregations can only be built at the leaf level of a parent-child hierarchy.

If you already have a parent-child dimension built, then launch this feature from the right-click menu of that dimension in Solution Explorer:

![](Parent-Child Dimension Naturalizer_PCDimNaturalizerDimMenu.png)

You are then prompted with the following screen which lets you choose exactly how the naturalized dimension is built:

![](Parent-Child Dimension Naturalizer_PCDimNaturalizerDimScreen.png)

Upon clicking OK, and depending on the action level chosen, the SQL table behind the parent-child dimension is flattened and added to the DSV with the prefix "DimNaturalized_", the new naturalized dimension is built, it is added to the cube, and the dimension and cubes are processed using ProcessFull.


If you have not built a parent-child dimension yet, consider building one as the above option will save you lots of work. If you choose not to build a parent-child dimension and then naturalize it, you can still have *{{site.title}}* create you a SQL view with the flattened parent-child dimension table. This option can be launched from the right-click context menu on the DSV:

![](Parent-Child Dimension Naturalizer_PCDimNaturalizerDsvMenu.png)

You are then prompted with the following screen which lets you choose the parent-child table to flatten:

![](Parent-Child Dimension Naturalizer_PCDimNaturalizerSqlScreen.png)

Upon clicking Naturalize, the flattened SQL table is created and added to the DSV with the prefix "DimNaturalized_".


Please see the [Parent-Child Dimension Naturalizer project](http://www.codeplex.com/PCDimNaturalize) for more documentation on exactly what's happening under the covers.

#### Limitations

* Currently secondary data sources are not supported. Secondary data sources occur when the primary data source for the DSV is one data source, but the DSV table in question comes from a second data source.