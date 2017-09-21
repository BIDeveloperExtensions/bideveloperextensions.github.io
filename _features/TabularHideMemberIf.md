---
title: Tabular HideMemberIf
category: ssas
component: ssast
---

_**Note:** this feature is NOT supported in the 1200 compatibility mode for SSAS Tabular 2016 as Microsoft removed the undocumented hooks that we were using to expose this functionality. However, SSAS Tabular 2017 supports this feature [natively](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/whats-new-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/)._

SQL Server Data Tools 2012 (formerly BI Development Studio) Tabular projects allow adding hierarchies to tables. However, a UI for setting the HideMemberIf property is not provided. This prevents Tabular projects from creating ragged hierarchies. For example, in the Adventure Works Employee hierarchy, Stephen Jiang not only is a manager, but has also sold some products. Without setting HideMemberIf, a blank shows up in the hierarchy (left PivotTable). After setting HideMemberIf on Level3 to NoName, the blank employee name row drops out as desired (right PivotTable):

![](Tabular HideMemberIf_HideMemberIfPivot.png)

Warning: While the HideMemberIf setting works in Tabular models, it is not officially supported by Microsoft. If you encounter a bug in how Tabular handles HideMemberIf and open a support case, Microsoft may not provide support. For example, there are reports that Tabular HideMemberIf will cause Visual Studio to [workitem:hang](http://bidshelper.codeplex.com/workitem/35428). There are other reports that [workitem:HideMemberIf doesn't work in PerformancePoint](http://bidshelper.codeplex.com/workitem/33002) with Tabular models.

In order to set HideMemberIf, switch to the diagram view where you manage hierarchies. Highlight one or more levels then right click and choose Set HideMemberIf...

![](Tabular HideMemberIf_TabularHideMemberIfMenu.png)

When the dialog pops up set HideMemberIf. When you click OK the change is applied to the workspace database immediately. ProcessFull is required during this operation due to a bug in SSAS 2012.

![](Tabular HideMemberIf_HideMemberIfDialog.png)

Note that some changes like renaming levels will wipe out the HideMemberIf setting. *{{site.title}}* backs up the HideMemberIf setting in an annotation on the database. That way, the [Tabular Pre-Build](../TabularPre-Build) feature can prompt you to fix this setting.

After changing a HideMemberIf setting, *{{site.title}}* may prompt you for the credentials to a data source which is using stored credentials if you have not already entered those credentials during this SSDT editing session. This prompt ensures that Tabular HideMemberIf succeeds (since it needs to ProcessFull the table) and also that data source credentials in the workspace database do not get wiped out as HideMemberIf settings are applied.