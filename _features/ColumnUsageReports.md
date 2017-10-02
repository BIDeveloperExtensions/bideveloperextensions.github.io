---
title: Column Usage Reports
category: ssas
component: 
    - ssasm
    - ssast
compatibilitylevel:  
    - 1103
    - 1200
    - 1400
---

Right-clicking on the DSV of an Analysis Services Multidimensional project lets you open two reports about column usage:

![](Column Usage Reports_UnusedColumnsTeaser.png)

**Unused Columns Report**
This report lists all columns in the DSV which are not used in dimensions, cubes, or mining structures. Download a [sample](Column Usage Reports_UnusedColumns.pdf). Double-checking columns on this report is a quick way to identify whether you accidentally missed any columns when designing the cube. Keep in mind, though, the general best practice is only to add columns to the cube that are needed for analysis.

**Used Columns Report**
This report lists all columns in the DSV which are used in dimensions, cubes, or mining structures. Download a [sample](Column Usage Reports_UsedColumns.pdf). This report can be used for proofreading the setup of your cube or for documentation.


#### Tabular Models
Starting with release 1.6.5, the Unused Columns Report is available for Analysis Services Tabular models. Right click in Solution Explorer on the .bim file to launch this report.

![](Column Usage Reports_UnusedColumnsReportMenuTabular.png)

As discussed in the [Tabular Performance Guide](http://aka.ms/ASTabPerf2012), when processing a Tabular model, Analysis Services runs the SQL query as provided by the developer. This causes any unused columns to be retrieved, slowing model processing. For Tabular models, the Unused Columns Report helps alert the developer of this problem. (Multidimensional models are different in that when Analysis Services processes a Multidimensional cube, it requests only the columns needed, so unused columns don't slow down Multidimensional model processing.)

Limitation: Note that only the query defined in the Edit Table Properties dialog is checked for unused columns. The partition queries are not parsed looking for unused columns.

The Used Columns Report is not shown for Tabular models. Due to the straightforward mapping of columns in the SQL queries to columns in the tables in your Tabular model, it is not needed. Utilize the Edit Table Properties dialog to see a mapping of the columns in the SQL query to the column names in the model if needed.