---
title: Delete Dataset Cache Files
category: ssrs
component: ssrs
---

In the report designer in {{site.ms-designer}}, when you are previewing a report, the dataset gets cached to disk as a .rdl.data file to improve performance. However, this cache can prevent you from seeing new changes to data in the data source. The resolution is to delete the .rdl.data files. *{{site.title}}* automates this for you.

Right-clicking on a Reporting Services 2005 or 2008 project node displays the following menu item. When you click it, *{{site.title}}* deletes any .rdl.data files that correspond to reports in that project.

![](Delete Dataset Cache Files_DeleteDatasetCacheFilesMenu.png)
