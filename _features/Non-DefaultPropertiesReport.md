---
title: Non-Default Properties Report
category: ssis & ssas
component: 
    - ssasm
    - ssis
---

Ever inherited someone's work and wondering what unexpected settings are used? The Non-Default Properties Report will let you see on one screen all properties which have been changed from their defaults. The report can be run for Analysis Services or for Integration Services:

#### Analysis Services

Right-clicking on the database node in Solution Explorer reveals the Non-Default Properties Report menu option:

![](Non-Default Properties Report_NonDefaultPropertiesSSASProjectMenu.png)

When chosen, a dialog opens showing all properties that were scanned that had non-default values. Uncheck the properties you do not wish to see then click OK. The properties you unchecked will be remembered so that you do not have to uncheck them the next time.

![](Non-Default Properties Report_NonDefaultPropertiesSelectorSSAS.png)

The report's first page is a table of contents which groups by property. Expanding a property lets you see all the objects which contain a non-default value on this property. This is helpful if you want to know, for example, which measures have MeasureExpression's. Clicking an object path takes you to the details on a later page.

![](Non-Default Properties Report_NonDefaultPropertiesReportSSAS_TOC.png)

The next pages of the report group by object. For each property, you see the default value and the current value.

![](Non-Default Properties Report_NonDefaultPropertiesReportSSAS.png)

Exporting the report to Excel correctly renders the table of contents. You can download a [sample export](Non-Default Properties Report_NonDefaultPropertiesSSAS.xls) of this report against Adventure Works DW.


#### Integration Services

The equivalent report for SSIS packages can be launched from one of three places in solution explorer: from the solution node, from the project node, or from an individual package.

When chosen, a dialog opens showing all properties that were scanned that had non-default values. Uncheck the properties you do not wish to see then click OK. The properties you unchecked will be remembered so that you do not have to uncheck them the next time.

![](Non-Default Properties Report_NonDefaultPropertiesSelectorSSIS.png)

The properties which are scanned were chosen very carefully. For instance, no DateTime properties (like CreationDate) are scanned because the value is always going to be different than the “default”. Also, almost no plain-text string properties were scanned because they are usually SQL commands or other such properties which are always different than the default.

The report's first page is a table of contents which groups by property. Expanding a property lets you see all the objects which contain a non-default value on this property. This is helpful if you want to know, for example, which tasks have changed the TransactionOption property. Clicking an object path takes you to the details on a later page.

The next pages of the report group by object. For each property, you see the default value and the current value. Unlike Analysis Services in which the object model is decorated with a DefaultValueAttribute denoting the proper default, the Integration Services object model does not have similarly denoted default values. In order to determine the default, a temporary package and task are created behind the scenes and the "default" property values are noted.

Exporting the report to Excel correctly renders the table of contents. You can download a [sample export](Non-Default Properties Report_NonDefaultPropertiesSSIS.xls) of this report against a demonstration package.


If there are any properties which are not showing up on this report which you feel should be showing up, please post an issue on the [Issue Tracker]({{site.github.issues_url}}) tab.