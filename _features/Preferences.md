---
title: Preferences
component: common
---

Several *{{site.title}}* features can be configured via a Preferences screen. To get to this screen, go to the Tools menu, choose Options, then find the *{{site.title}}* section and the Preferences tab under it.

![](Preferences_Preferences.png)

The [Smart Diff](../SmartDiff) setting is to allow you to use third-party command line programs like [Beyond Compare](http://www.scootersoftware.com) as the diff viewer in [Smart Diff](Smart-Diff)(Smart-Diff) instead of TFS or VSS.

To pass the 2 versions of a file to your diff tool after they have been processed by SmartDiff you need to insert a question marks (?) where the argument for the left and right files normally go.

So an example custom command line for Beyond Compare may look like the following:

```
"C:\Program Files (x86)\Beyond Compare 4\bcomp.exe" ? ?
```

The [Expression and Configuration Highlighter](../ExpressionandConfigurationHighlighter) setting is meant for people with color-blindness to be able to choose the colors used to highlight expressions and configurations in SSIS packages.

The [Measure Group Health Check](../MeasureGroupHealthCheck) setting called Free Space Factor works in the following way. If the measure currently contains 1 million rows, a free space factor of 20 means that Measure Group Health Check will pick a datatype that will hold a value of 20 million.