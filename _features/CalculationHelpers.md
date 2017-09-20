---
title: Calculation Helpers
category: ssas
component: ssasm
---

This feature enhances the Calculations tab of the cube editor.

First, it remembers whether you work in the Script View or the Form View and takes you to that view immediately upon opening the Calculations tab of the cube editor.

Second, this feature improves the Calculation Properties dialog in several ways. The Microsoft version [required](https://connect.microsoft.com/SQLServer/feedback/ViewFeedback.aspx?FeedbackID=249650) that you close and reopen the cube designer window before it would pick up any new calculated measures you added to the calc script. This problem is solved with the *{{site.title}}* add-in. *{{site.title}}* also allows you to [edit descriptions](https://connect.microsoft.com/SQLServer/feedback/ViewFeedback.aspx?FeedbackID=127157) on calculated measures and named sets via the UI. Previously, editing these descriptions was only possible via direct editing of the *.cube XML file.

*{{site.title}}* replaces the existing Calculation Properties button with its own:

![](Calculation Helpers_CalculationPropertiesButtonTeaser.gif)

The Calculation Properties window that appears when you click that button is identical to the Microsoft one, except that it adds an "Edit Description" button:

![](Calculation Helpers_CalculationPropertiesDescriptionsTeaser.gif)

