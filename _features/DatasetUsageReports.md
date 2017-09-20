---
title: Dataset Usage Reports
category: ssrs
component: ssrs
---
### Dataset Usage Reports

All datasets in Reporting Services reports are executed, regardless of whether they are all used. Identifying unused datasets can allow you to delete the unused datasets, thus speeding report performance and scalability. Also, identifying where in a report datasets are used can help you understand an unfamiliar report. This *{{site.title}}* feature lets you view a list of used and unused Reporting Services datasets.

Right-clicking on the project node or the solution node of any Visual Studio 2005 or 2008 project with .rdl or .rdlc files (e.g. C# projects with .rdlc files, not just SSRS projects) reveals the following menu:

![](Dataset Usage Reports_UnusedDatasetsMenu.png)

**Unused Report Datasets...**
This report lists all Reporting Services datasets which are not used anywhere in the report.

**Used Report Datasets...**
This report lists all Reporting Services datasets which are used. It lists which parts of the report use this dataset. Download a [sample](Dataset Usage Reports_UsedDatasets.xls) showing the results of this feature run against the Adventure Works sample reports, or look at the following screenshot:

![](Dataset Usage Reports_UsedDatasetsReport.png)

**Notes:**
* This feature runs entirely offline without touching ReportServer and without connecting to any of your datasources. It simply navigates the XML in the RDL file and parses expressions.
* Sanity check any dataset that *{{site.title}}* reports as unused before deleting it. If you do encounter any datasets that *{{site.title}}* incorrectly identifies as unused, please [create an issue](/issues) and attach the RDL file.
