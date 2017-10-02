---
title: Printer Friendly Dimension Usage
category: ssas
component: 
    - ssasm
    - ssast
compatibilitylevel:  
    - 1103
    - 1200
    - 1400
---

The Dimension Usage tab allows you to define the relationships between dimensions and measure groups. The Printer Friendly Dimension Usage feature allows you to view and print a report encompassing all the information from that Dimension Usage tab. To use this feature, right click on the cube in Solution Explorer:

![](Printer Friendly Dimension Usage_PrinterFriendlyDimensionUsageTeaser.gif)

Starting with *{{site.title}}* 1.7, for Tabular models, right click on the .bim file to launch this report.

Then a report similar to the following will open:

![](Printer Friendly Dimension Usage_PrinterFriendlyDimensionUsageReport.gif)

You can download a [sample copy](Printer Friendly Dimension Usage_PrinterFriendlyDimensionUsage.pdf) of this report run against the Adventure Works cube.

Starting with release 1.6.4, when you run this feature, it first prompts you to ask if you want the detailed view (the report seen above) or a Bus Matrix view which looks like the following:

![](Printer Friendly Dimension Usage_BusMatrix.png)

We recommend you export this report to Excel if you desire to do further formatting such as rotating the column labels. You can download a [sample copy](Printer Friendly Dimension Usage_PrinterFriendlyDimensionUsageBusMatrix.xls) Excel Bus Matrix report which was run against the Adventure Works cube.