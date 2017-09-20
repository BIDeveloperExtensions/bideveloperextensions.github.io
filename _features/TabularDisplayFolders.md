---
title: Tabular Display Folders
category: ssas
component: ssast
---
*Note: this feature is only enabled for models in the 1103 compatability mode. For models in 1200 or later you should use the native functionality in SSDT*

Unlike Multidimensional projects, Tabular projects in SQL 2012 do not support display folders. This feature gap makes Tabular models less user-friendly since the field list in Excel PivotTables is longer and less organized than it could be.

Warning: While display folders work in Tabular models, they are not officially supported by Microsoft. If you encounter a bug in how Tabular handles display folders and open a support case, Microsoft may not provide support.

*{{site.title}}* provides a UI for editing display folders on measures, columns, and hierarchies. All display folders are edited in the same place. Right click on the .bim file and choose Tabular Display Folders...

![](Tabular Display Folders_TabularDisplayFoldersMenu.png)

That launches the UI for editing display folders:

![](Tabular Display Folders_TabularDisplayFolders.png)

Tips:

* If a field is showing up under the "More fields" folder in the Excel field list, setting the display folder to a backslash (i.e. \ ) will cause it to show up under the root of the table, not under the "More fields" folder.
	* Unfortunately an SSAS [bug](https://connect.microsoft.com/SQLServer/feedback/details/792403/attributehierarchydisplayfolder-of-backslash-lost-on-xmla-alter) is preventing the backslash trick from working when the SSAS server is on AS2012 SP1 CU4 (confirmed on that version... not sure if it impacts other versions of SSAS)
* Some client tools like Excel allow a field to show under multiple folders. In order to accomplish this, separate the two folders with a semicolon (i.e. Folder1\SubFolder1;Folder2)


Limitations:

* Note that some changes like reordering levels or setting format strings will wipe out the display folders. *{{site.title}}* backs up the display folders in an annotation on the database. That way, the [Tabular Pre-Build](../TabularPre-Build) feature can prompt you to fix this setting.

* Display folders are not supported in all DAX clients 
	* Power View for SharePoint will show display folders if you have SQL 2012 SP1 CU4 or later installed 
	* Power View in Excel 2013 currently ignores display folders (all measures are displayed in a flat list)

* Display folders are not supported on Tabular KPIs currently due to a [bug](https://connect.microsoft.com/SQLServer/feedback/details/706895/translations-dont-work-for-kpis-created-in-mdx-script) in Analysis Services.


After changing display folders, *{{site.title}}* may prompt you for the credentials to a data source which is using stored credentials if you have not already entered those credentials during this SSDT editing session. This prompt ensures that data source credentials in the workspace database do not get wiped out as display folder settings are applied.