---
title: Create Fixed Width Columns
layout: feature
category: ssis
component: ssis
---

Defining the layout of a fixed-width flat file connection manager can be very tedious. Most times when you are importing a fixed-width flat file, you have an accompanying Excel spreadsheet which defines the column names and widths. The Create Fixed Width Columns feature of *{{site.title}}* allows you to use your Excel spreadsheet to create the column definitions in a few simple steps.

First, create a connection manager for a flat file, and set the Format to "Fixed width" or "Ragged right". Then flip to the Columns screen and click OK (to save this connection manager with the default one column). Then right-click on the connection manager and choose "Create Fixed Width Columns":

![](Create Fixed Width Columns_FixedWidthColumnsMenu.png)

Next, a screen pops up and asks you to paste information from Excel. Follow the instructions on the screen then click OK once you're satisfied with the column definitions you've pasted into the grid on the screen:

![](Create Fixed Width Columns_FixedWidthColumns.png)

Finally, if you have any columns that should be a datatype other than string, edit the connection manager, flip to the Advanced screen, and click the "Suggest Types..." button.