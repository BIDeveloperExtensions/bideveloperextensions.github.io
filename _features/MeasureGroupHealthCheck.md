---
title: Measure Group Health Check
category: ssas
component: ssasm
---

This feature allows you check various indications of measure group health. Currently, this feature only checks one indication of health:

* Checks the measure datatype to determine if there could be an overflow.

![](Measure Group Health Check_MeasureGroupHealthCheckTeaser.gif)

In designing the fact table in a SQL database, it is a common practice to choose the smallest possible datatype. That datatype need only be big enough to hold the largest single value. However, in Analysis Services, the measure datatype needs to be big enough to hold the largest aggregated value. If an aggregation overflows the measure's datatype, [bad things happen](http://geekswithblogs.net/darrengosbell/archive/2006/11/27/99190.aspx). Determining what datatype is most appropriate as the measure datatype requires profiling the data in the fact table with SQL queries. Measure Group Health Check automates this process.

To launch this feature, right click on the measure group in the Cube Structure tab of the cube designer:

![](Measure Group Health Check_MeasureGroupHealthCheckMenu.gif)

Immediately, *{{site.title}}* will execute a single SQL query that builds a profile of the measure data by getting the totals for each measure across the entire fact table. Depending on the size of the fact table, this query could be very slow, and it cannot be cancelled currently. We recommend saving all your work in {{site.ms-designer}} in case you need to kill the devenv.exe process to cancel the query. The query inherits the Query Timeout setting from the datasource, though, so we recommend changing that property appropriately. (Set it to 0 if you want it to finish no matter how long it takes, or set it to the maximum amount of time you're willing to wait before you run the measure group health check.)

The Measure Group Health Check dialog above colors any measures where it is recommending a measure datatype change. The dialog provides you all the information you need to decide on datatypes. The following columns are shown:

* _Measure_ - The measure name
* _Aggregate_ - The aggregate function for that measure.
* _Total_ - The aggregated value across all rows. The aggregate function for this measure controls how the data is aggregated. Note that the AverageOfChildren, ByAccount, FirstChild, FirstNonEmpty, LastChild, and LastNonEmpty aggregate functions are treated just like Sum for the purposes of the measure group health check.
* _Min_ - The minimum value from a single row. Mainly this column is used to indicate whether this column contains any negative values.
* _Max_ - The maximum value from a single row. Mainly this column is used to let you estimate the worst-case total value if in the future every row contained a very large value.
* _Decimals?_ - Are there any rows in which this column has decimals? Mainly this column is used to indicate whether the integer family of datatypes will be appropriate. If this column reports "4+" that means that the Currency datatype will not be appropriate since it only supports 4 decimal places.
* _DSV_ - The datatype for the column in the data source view expressed as a .NET type. Click on the ? button in this dialog to see a mapping of SSAS to .NET types. Mainly this column is used to let you ensure that you choose a measure datatype which is at least as large as the DSV column datatype.
* _Current_ - The current measure datatype.
* _New_ - This column is a combo box showing only valid datatypes which would not result in an overflow or a loss of precision on the current fact table data. You should choose the new measure datatype for each measure before clicking the OK button. This column defaults to the recommended new measure datatype. Any time the recommendation is different than the current measure datatype, the row is colored. The recommended datatype will be the smallest possible datatype to satisfy all these conditions:
  - The recommendation must be a valid datatype which would not result in an overflow or a loss of precision on the current fact table data.
  - The recommendation cannot be a smaller datatype than the DSV column datatype.
  - The recommendation must allow for 20x growth of the fact table without an overflow. (Starting in release 1.4.2.2, you can edit that 20x setting in the [Preferences](../Preferences) screen.)

When you click the OK button, any measures where the New column doesn't match the Current column are updated in the cube designer. Only the measure's column binding datatype and measure datatype are changed. Nothing in the DSV needs to be changed.

_Limitations:_
* In the 1.2 release, SQL Server and Oracle are the supported datasources. The 1.3.0.8 release supports Teradata datasources, too.
* Measure expressions are ignored.
* DateTime datatype measures are skipped (unless they are Count or Distinct Count measures).
* The AverageOfChildren, ByAccount, FirstChild, FirstNonEmpty, LastChild, and LastNonEmpty aggregate functions are treated just like Sum for the purposes of the measure group health check.
* Nothing in the calc script is taken into account. If you make scoped assignments which can subsequently aggregate, an overflow can still occur if the correct measure datatype is not set on the measure.
* *{{site.title}}* Measure Group Health Check never recommends the Single datatype because it only allows 7 decimals of precision.

_Tip:_ You can copy the data from the measure group health check dialog with Ctrl-A then Ctrl-C and then paste it into Excel. This makes good basic documentation of a fact table. It is also good to monitor fact table size over time and plan for capacity and stay ahead of overflows.

_Tip:_ After you refresh the DSV, run Measure Group Health Check on any affected measure groups to quickly check whether any measure datatypes need to change.

_Tip:_ Review this [whitepaper](http://sqlcat.com/technicalnotes/archive/2008/09/25/the-many-benefits-of-money-data-type.aspx) on the Currency datatype and use it where possible.