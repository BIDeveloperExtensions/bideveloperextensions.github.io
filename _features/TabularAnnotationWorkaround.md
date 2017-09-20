---
title: Tabular Annotation Workaround
category: ssas
component: ssast
---

After upgrading to SQL Server 2012 SP1 SSDT, some users have complained about receiving an error that prevents them from opening the .bim file in a Tabular model:

```
============================
Error Message:
============================

An error occurred while opening the model on the workspace database. Reason: ReadElementContentAs() methods cannot be called on an element that has child elements.

============================
Call Stack:
============================

 at Microsoft.AnalysisServices.VSHost.VSHostManager.PrepareSandbox(Boolean newProject, Boolean& isRefreshNeeded, Boolean& isImpersonationChanged, Boolean& saveRequired, List`1& truncatedTables, Boolean isRealTimeMode, Int32 clientCompatibilityLevel)
 at Microsoft.AnalysisServices.VSHost.Integration.EditorFactory.CreateEditorInstance(UInt32 grfCreateDoc, String pszMkDocument, String pszPhysicalView, IVsHierarchy pvHier, UInt32 itemid, IntPtr punkDocDataExisting, IntPtr& ppunkDocView, IntPtr& ppunkDocData, String& pbstrEditorCaption, Guid& pguidCmdUI, Int32& pgrfCDW)

============================
```


This problem is a bug in SSDT in that it does not properly parse annotations created by *{{site.title}}*. 

**_UPDATE:_** This SSDT bug has been [fixed](http://support.microsoft.com/kb/2806601) in [SQL2012 SP1 CU3](http://support.microsoft.com/kb/2812412). 

If you are experiencing this issue you have two options:

1. Install [SQL2012 SP1 CU3](http://support.microsoft.com/kb/2812412)
2. Install *{{site.title}}* 1.6.2 and use a workaround utility which changes the storage format for *{{site.title}}* annotations. *{{site.title}}* release 1.6.2 includes this workaround feature described below.

If you choose to use the *{{site.title}}* workaround utility instead of installing CU3, do the following. With the .bim file **closed**, right click on the .bim file and select Tabular Annotation Workaround...

![](Tabular Annotation Workaround_TabularAnnotationWorkaroundMenu.png)

This feature will popup a confirmation dialog. Read it carefully, especially the note about every developer on your team upgrading to the latest version of *{{site.title}}*.

![](Tabular Annotation Workaround_TabularAnnotationWorkaround.png)

As background on this issue, see the Connect issue [here](https://connect.microsoft.com/SQLServer/feedback/details/776444/tabular-model-error-during-opening-bim-after-sp1-readelementcontentas-methods-cannot-be-called-on-an-element-that-has-child-elements). 