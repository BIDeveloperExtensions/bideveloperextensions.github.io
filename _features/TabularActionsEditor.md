---
title: Tabular Actions Editor
category: ssas
component: ssast
compatibilitylevel: 1103
---

*Note: This feature is only available with models in the 1103 compatability mode*

This feature provides a UI for editing actions for Tabular models. For example, this feature allows the model designer the ability to customize the columns returned by drillthrough. This feature also allows the model designer to create report, URL, or rowset
 actions, for example.

Warning: While actions work in Tabular models, they are not officially supported by Microsoft. If you encounter a bug in how Tabular handles actions and open a support case, Microsoft may not provide support.

In a Tabular model (SQL Server 2012 and above only) right click the .bim file to find the menu item to launch this feature:

![](Tabular Actions Editor_TabularActionEditorMenu.png)

The *{{site.title}}* Tabular Actions Editor dialog will pop up. To create your first action, click the Add button.&nbsp;Create your actions and click OK. When you click OK, the actions are deployed to the workspace database (just like all other editing of the
 Tabular model).

### Perspectives

Note that you can assign actions to perspectives using this dialog. The Perspectives dialog currently does not support actions, so *{{site.title}}* built its own support in this actions dialog. Most common clicks like adding or removing a table or column from
 a perspective in the Perspectives dialog will preserve the actions assignments. However, renaming a perspective usually wipes out the actions assignments to perspectives. For this reason, *{{site.title}}* backs up the action perspective assignments to an annotation.
 If you ever rename a perspective or create a new perspective, just open the *{{site.title}}* Actions Editor dialog and *{{site.title}}* will prompt you &quot;No actions are currently included in any perspectives, but *{{site.title}}* did retain a backup of the perspective assignments
 from the last actions editing session. Changes made to perspectives may have caused action assignments to be lost. Restoring action perspective assignments may be possible except when a perspective has been renamed. Would you like *{{site.title}}* to attempt restore
 the action perspective assignments now?&quot;. Clicking Yes will tell *{{site.title}}* to attempt a restore. The restore of the action perspective assignments should work except when a perspective has been renamed. Also, the
[Tabular Pre-Build](../TabularPre-Build) feature can prompt you to restore the perspective assignments.

### Internet Sales Drillthrough Example
Modeled after the Internet Details action from the Multidimensional sample Adventure Works cube, this action demonstrates&nbsp;how *{{site.title}}* can allow you to customize the columns returned from the default drillthrough command which is used when you double
 click a numeric cell from a PivotTable in Excel.&nbsp;Out of the box, Tabular models just return the columns from the fact table as the default drillthrough return columns. However, most fact tables contain only meaningless surrogate keys, necessitating this
 *{{site.title}}* UI for customizing drillthrough to show meaningful columns.

![](Tabular Actions Editor_TabularActionEditorInternetDetails.png)

| Property | Setting |
|---|---|
|Name |Internet Details|
|Caption|Drillthrough...|
|Caption is MDX?|Unchecked|
|Description| |
|Action Type|DrillThrough|
|Target Type|Cells|
|Target|MeasureGroupMeasures("Internet Sales")|
|Condition| |
|Drillthrough Columns|` [Customer].[First Name]  `<br/>` [Customer].[Last Name] `<br/>` [Date].[Date] `<br/>` [Product].[Product Name] `<br/>` [Sales Territory].[Sales Territory Region] `<br/>` [Sales Territory].[Sales Territory Country] `<br/>` [Promotion].[Promotion Name] `<br/>` [Internet Sales].[Sales Order Number] `<br/>`  [Internet Sales].[Sales Order Line Number] `<br/>` [Internet Sales].[Sales Amount] `<br/>` [Internet Sales].[Extended Amount] `<br/>` [Internet Sales].[Tax Amt] `<br/>` [Internet Sales].[Freight] `|
|Default|True|
|Maximum Rows| |
|Invocation|Interactive|


*Note: The MeasureGroupMeasures function [returns an empty set in Tabular models](https://connect.microsoft.com/SQLServer/feedback/details/699204/measuregroupmeasures-returns-an-empty-set-in-tabular-models) since there are no physical measures, only calculated measures. Plus, there is no way of setting the Target property of a drillthrough action to target more than one calculated measure. So behind the scenes, *{{site.title}}* creates one identical action per calculated measure. This means that when you add a new calculated measure, you need to open and close the *{{site.title}}* Tabular Actions Editor dialog so the drillthrough action can be targeted to this new calculated measure.*

*Note: In Tabular models, you cannot choose measures&nbsp;to be returned. Instead, you choose columns from the fact table or columns from the dimension tables.*

*Note: Once you have added a drillthrough column, to remove it, left click on the row header (i.e. the space to the left of the Table Name) and press delete. Or alternately right click on the row and choose delete from the context menu.*

*Note: The UI makes it impossible to add a drillthrough column twice. After you have used a column, it no longer appears in any other row as an option.*

### City Map Example

Modeled after the City Map action from the Multidimensional sample Adventure Works cube, this action demonstrates a URL action which allows a user to right click on a city and be taken to a mapping website showing that city.

![](Tabular Actions Editor_TabularActionEditorCityMap.png)

<table>
<tbody>
<tr>
<th>Property</th>
<th>Setting</th>
</tr>
<tr>
<td>Name</td>
<td>City Map</td>
</tr>
<tr>
<td>Caption</td>
<td>&quot;View Map for &quot; &#43; [Geography].[City].CurrentMember.Member_Caption &#43; &quot;...&quot;</td>
</tr>
<tr>
<td>Caption is MDX?</td>
<td>Checked</td>
</tr>
<tr>
<td>Description</td>
<td>This action will display the map for a given city.</td>
</tr>
<tr>
<td>Action Type</td>
<td>Url</td>
</tr>
<tr>
<td>Target Type</td>
<td>AttributeMembers</td>
</tr>
<tr>
<td>Target</td>
<td>[Geography].[City]</td>
</tr>
<tr>
<td>Condition</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Expression</td>
<td>
<p>// URL for linking to MSN Maps<br>
&quot;http://maps.msn.com/home.aspx?plce1=&quot; &#43;</p>
<p>// Retreive the name of the current city<br>
[Geography].[City].CurrentMember.Name &#43; &quot;,&quot; &#43;</p>
<p>// Append state-province name<br>
{Existing [Geography].[State Province Name].[State Province&nbsp;Name].Members}.Item(0).Name &#43; &quot;,&quot; &#43;</p>
<p>// Append country name<br>
{Existing [Geography].[English Country Region Name].[English Country Region Name].Members}.Item(0).Name &#43;</p>
<p>// Append region paramter <br>
&quot;&amp;regn1=&quot; &#43;</p>
<p>// Determine correct region paramter value<br>
Case<br>
&nbsp;&nbsp;&nbsp; When {Existing [Geography].[English Country Region Name].[English Country Region Name].Members}.Item(0) Is<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Geography].[English Country Region Name].&amp;[Australia]<br>
&nbsp;&nbsp;&nbsp; Then &quot;3&quot;<br>
&nbsp;&nbsp;&nbsp; When {Existing [Geography].[English Country Region Name].[English Country Region Name].Members}.Item(0) Is<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Geography].[English Country Region Name].&amp;[Canada]
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Or<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {Existing [Geography].[English Country Region Name].[English Country Region Name].Members}.Item(0) Is<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Geography].[English Country Region Name].&amp;[United States]<br>
&nbsp;&nbsp;&nbsp; Then &quot;0&quot;<br>
&nbsp;&nbsp;&nbsp; Else &quot;1&quot;<br>
End</p>
<p>// The &quot;plce1&quot; parameter represents a named location.<br>
// The &quot;regn1&quot; parameter indicates the region in which <br>
// the named location is located.</p>
<p>// 0 = North America<br>
// 1 = Europe<br>
// 2 = World Atlas<br>
// 3 = Australia<br>
// 4 = Brazil</p>
</td>
</tr>
<tr>
<td>Invocation</td>
<td>
<p>&nbsp;Interactive</p>
</td>
</tr>
</tbody>
</table>

*Note: The example above uses MDX for the Caption and Expression. If you want to use DAX, build a calculated measure into your model, then reference it as [Measures].[DAX Measure Name]&nbsp;in this actions dialog.*

### Sales Reason Comparisons Example
Modeled after the Sales Reason Comparisons action from the Multidimensional sample Adventure Works cube, this action demonstrates a report action which allows a user to right click on a Product Category and be taken to an SSRS report.

![](Tabular Actions Editor_TabularActionEditorSalesReasonComparisons.png)

<table>
<tbody>
<tr>
<th>Property</th>
<th>Setting</th>
</tr>
<tr>
<td>Name</td>
<td>Sales Reason Comparisons</td>
</tr>
<tr>
<td>Caption</td>
<td>&quot;Sales Reason Comparisons for &quot; &#43; [Product].[Category].CurrentMember.Member_Caption &#43; &quot;...&quot;</td>
</tr>
<tr>
<td>Caption is MDX?</td>
<td>Checked</td>
</tr>
<tr>
<td>Description</td>
<td>This action will launch a report comparing sales reasons for a given product category.</td>
</tr>
<tr>
<td>Action Type</td>
<td>Report</td>
</tr>
<tr>
<td>Target Type</td>
<td>AttributeMembers</td>
</tr>
<tr>
<td>Target</td>
<td>[Product].[Product Category Name]</td>
</tr>
<tr>
<td>Condition</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Report Parameters</td>
<td>
<table>
<tbody>
<tr>
<th>Parameter Name</th>
<th>Parameter Value Expression</th>
</tr>
<tr>
<td>ProductCategory</td>
<td>UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )</td>
</tr>
<tr>
<td>rs:Format</td>
<td>&quot;EXCEL&quot;</td>
</tr>
</tbody>
</table>
</td>
</tr>
<tr>
<td>Report Server</td>
<td>localhost</td>
</tr>
<tr>
<td>Report Path</td>
<td>ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons</td>
</tr>
<tr>
<td>Invocation</td>
<td>Interactive</td>
</tr>
</tbody>
</table>

**Important Note: In SSAS 2016 it appears Report Server needs to include http:// or https:// before the server name.**

*Note: The example above uses MDX for the Caption and Report Parameter Value Expression. If you want to use DAX, build a calculated measure into your model, then reference it as ```[Measures].[DAX Measure Name]``` in this actions dialog.*

*Note: rs:Command=Render is not shown on the screen but is included in the action's ReportFormatParameters behind the scenes.*

*Note: In addition to specifying report parameters, you can also specify other [URL commands](http://msdn.microsoft.com/en-us/library/ms152835(v=SQL.110).aspx) like the rs:Format command. You must use an MDX expression for rs:Format (and all other report parameters), so if you want to hardcode it, put double quotes around the literal e.g. 'EXCEL').*

*Note: If SSRS is in **SharePoint integrated mode** you can use the above example, though the report path would need to be the URL to the report (e.g. _vti_bin/ReportServer?http://localhost/sites/bi/Reports/Report Library/AdventureWorks Sample Reports/Sales Reason Comparisons.rdl). Also note that SSRS 2012 in SharePoint Integrated Mode puts the ReportServer URL under /_vti_bin/ReportServer.*

*Note: If SSRS is in **SharePoint integrated mode** and you wish to render the report in HTML with the SharePoint site branding surrounding it like when you run a report directly from SharePoint, note the [URL commands](http://blogs.msdn.com/b/prash/archive/2009/01/21/passing-url-report-parameters-to-reports-in-sharepoint-document-library-in-ssrs-2008.aspx) are different. So an example SSRS SharePoint integrated mode report action might look like the following.*


### SharePoint Integrated Mode Report Action Example with SharePoint Branding

<table>
<tbody>
<tr>
<th>Property</th>
<th>Setting</th>
</tr>
<tr>
<td>Name</td>
<td>Sales Reason Comparisons</td>
</tr>
<tr>
<td>Caption</td>
<td>&quot;Sales Reason Comparisons for &quot; &#43; [Product].[Category].CurrentMember.Member_Caption &#43; &quot;...&quot;</td>
</tr>
<tr>
<td>Caption is MDX?</td>
<td>Checked</td>
</tr>
<tr>
<td>Description</td>
<td>This action will launch a report comparing sales reasons for a given product category.</td>
</tr>
<tr>
<td>Action Type</td>
<td>Report</td>
</tr>
<tr>
<td>Target Type</td>
<td>AttributeMembers</td>
</tr>
<tr>
<td>Target</td>
<td>[Product].[Product Category Name]</td>
</tr>
<tr>
<td>Condition</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Report Parameters</td>
<td>
<table>
<tbody>
<tr>
<th>Parameter Name</th>
<th>Parameter Value Expression</th>
</tr>
<tr>
<td>rp:ProductCategory</td>
<td>UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )</td>
</tr>
<tr>
<td>rv:ParamMode</td>
<td>&quot;Hidden&quot;</td>
</tr>
</tbody>
</table>
</td>
</tr>
<tr>
<td>Report Server</td>
<td>localhost</td>
</tr>
<tr>
<td>Report Path</td>
<td>sites/bi/Reports/_layouts/ReportServer/RSViewerPage.aspx?rv:RelativeReportUrl=/sites/bi/Reports/Report Library/AdventureWorks Sample Reports/Sales Reason Comparisons.rdl</td>
</tr>
<tr>
<td>Invocation</td>
<td>Interactive</td>
</tr>
</tbody>
</table>

**Important Note: In SSAS 2016 it appears Report Server needs to include http:// or https:// before the server name.**

### DAX Query Rowset Action Example
The following action demonstrates how to create an action which returns a rowset when you right click on a Sales Territory Region and execute the action.

![](Tabular Actions Editor_TabularActionEditorDAXQuery.png)

<table>
<tbody>
<tr>
<th>Property</th>
<th>Setting</th>
</tr>
<tr>
<td>Name</td>
<td>DAX Query Rowset</td>
</tr>
<tr>
<td>Caption</td>
<td>&quot;Reseller Sales In &quot; &#43; [Sales Territory].[Sales Territory Region].CurrentMember.Name &#43; &quot; Sales Territory...&quot;</td>
</tr>
<tr>
<td>Caption is MDX?</td>
<td>Checked</td>
</tr>
<tr>
<td>Description</td>
<td>This action will display a rowset with the Reseller Sales for this Sales Territory Region</td>
</tr>
<tr>
<td>Action Type</td>
<td>Rowset</td>
</tr>
<tr>
<td>Target Type</td>
<td>AttributeMembers</td>
</tr>
<tr>
<td>Target</td>
<td>[Sales Territory].[Sales Territory Region]</td>
</tr>
<tr>
<td>Condition</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Expression</td>
<td>
<p>&quot;<br>
Evaluate(<br>
&nbsp;CalculateTable(<br>
&nbsp; 'Reseller Sales'<br>
&nbsp; ,'Sales Territory'[Sales Territory Id] = &quot; <br>
&#43; {Existing [Sales Territory].[Sales Territory Id].[Sales Territory Id].Members}.Item(0).Name<br>
&#43; &quot;<br>
&nbsp;)<br>
)<br>
&quot;</p>
</td>
</tr>
<tr>
<td>Invocation</td>
<td>
<p>&nbsp;Interactive</p>
</td>
</tr>
</tbody>
</table>


*Note: The example above uses MDX for the Caption and Expression. If you want to use DAX, build a calculated measure into your model, then reference it as [Measures].[DAX Measure Name]&nbsp;in this actions dialog.*

*Note: The Expression is an MDX expression that's building a string. The string is a query that can run against Analysis Services. In this case, the string is a DAX query.*


Instead of a DAX query, you may want to construct a drillthrough query. This approach is especially helpful when you have already customized the default drillthrough columns for the Reseller Sales measure group (for example) by creating a drillthrough action flagged as Default. The expression in this case would be:

```
"drillthrough
select
from  [" + Measures].CurrentMember.Properties("CUBE_NAME") + "]
where (
[Measures].[Reseller Total Sales]," 
+ {
    Existing [Sales Territory].[Sales Territory Id].[Sales Territory Id].Members
  }.Item(0).UniqueName + ")"
```

*Note: The example above uses [Measures].CurrentMember.Properties('CUBE_NAME') to determine the name of the current cube. When developing against the workspace database, the main cube is named Sandbox, but using the project properties dialog, you can customize the name of the main cube when the solution is deployed. So be sure to test these actions against the workspace database and against the deployed database.*


### Measure Definitions Rowset Action

Another possible way to use actions is to provide users with a way of viewing measure definitions from within an Excel PivotTable. For example, if the Description property of measures has been filled in when developing your Tabular model, the following rowset action may be useful:

![](Tabular Actions Editor_TabularActionMeasureDefinition.png)

The action expression returns a string which is a DMV query:

```
"select
  [MEASURE_CAPTION]
, [MEASUREGROUP_NAME]
, [MEASURE_DISPLAY_FOLDER]
, [DESCRIPTION]
, [EXPRESSION]
from $SYSTEM.MDSCHEMA_MEASURES
where [MEASURE_UNIQUE_NAME] = '" + [Measures].CurrentMember.UniqueName + "'"
AND [CUBE_NAME] = '" + [Measures].CurrentMember.Properties("CUBE_NAME") + "'"
```

When you launch this action by right-clicking on a measure numeric value in a PivotTable and choosing this action, Excel opens a new tab and displays the following measure definition:

![](Tabular Actions Editor_TabularActionMeasureDefinitionResults.png)

### Other Examples

Darren Gosbell [posted a complex and powerful example](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/0164ce52-071b-4f74-a1b2-9113e5b0f63e/drilling-down-on-cumulative-measures?forum=sqlanalysisservices#ddb54608-b936-455b-83c1-01d526a3eea2) of determining the context and building a custom DAX query in a rowset action.
