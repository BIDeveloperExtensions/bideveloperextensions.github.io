---
title: Tabular Pre-Build
category: ssas
component: ssast
---

The SQL Server Data Tools 2012 editor will often destroy changes to Tabular models. For example, adding a new perspective may remove actions from perspectives. And renaming a level may lose the HideMemberIf setting set by *{{site.title}}*.

The Tabular Pre-Build feature catches the build event and checks features for *{{site.title}}* settings that have been lost. Because these settings were backed up in annotations, they can be restored, and the user will be prompted if this is necessary.

To ensure this feature is run, first ensure the .bim file is open so that the Tabular editor window is visible, then perform a Build or Deploy on the Tabular model:

![](Tabular Pre-Build_TabularPreBuildPlugin.png)

