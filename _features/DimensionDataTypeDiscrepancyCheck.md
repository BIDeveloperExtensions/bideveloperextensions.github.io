---
title: Dimension Data Type Discrepancy Check
category: ssas
component: ssasm
---

This feature allows you check that DSV data types match the data types on the KeyColumns and NameColumn of dimension attributes. It displays any discrepancies and lets you fix them with the click of a button:

![](Dimension Data Type Discrepancy Check_DataTypeDiscrepancyCheckWindow.gif)

The main scenario this feature is designed to help with is as follows. If you build a dimension attribute off a varchar(100) column, then you lengthen that column to varchar(200) in the SQL database, then refresh your DSV, that length change doesn't get replicated to the KeyColumn or NameColumn of dimension attributes which still have a DataSize property of 100. If any data in that column is longer than 100, you will receive an error during cube processing that says, "The size specified for a binding was too small, resulting in one or more column values being truncated."

To launch this feature, right click on the Dimensions folder in Solution Explorer:

![](Dimension Data Type Discrepancy Check_DataTypeDiscrepancyCheckMenu.gif)

When the window pops up (seen above), the following columns are shown:
* **Save?** - Uncheck this checkbox if you do not wish to have *{{site.title}}* make this data type or length change. Then click the OK button.
* **Dimension** - The name of the dimension containing the dimension attribute which has the data type discrepancy.
* **Attribute** - The name of the dimension attribute which has the data type discrepancy.
* **Column Type** - Displays either KeyColumn or NameColumn to indicate which has a data type discrepancy.
* **DSV Column** - The name of the column in the data source view which has a data type discrepancy.
* **DSV Data Type** - The data type of the column in the data source view.
* **DSV Length** - The length of the column in the data source view.
* **Old Data Type** - The old data type on the column binding (KeyColumn or NameColumn) on the dimension attribute.
* **Old Length** - The old data type length on the column binding (KeyColumn or NameColumn) on the dimension attribute.
* **New Data Type** - The new data type on the column binding (KeyColumn or NameColumn) on the dimension attribute.
* **New Length** - The new data type length on the column binding (KeyColumn or NameColumn) on the dimension attribute.

Take special notice of any rows which are red. Those rows represent data type (not just length) changes which may cause cells on the Dimension Usage tab to become invalid. After clicking the OK button to have *{{site.title}}* change the data types on the dimension attributes, you'll need to open the Dimension Usage tab on all your cubes and look for red squiggly lines. If there are any errors, first click the ... button in that cell to pop open the Define Relationship editor, then click OK. Wait a few seconds and see if the red squiggly goes away. If not, you may need to delete and recreate the relationship (click the ... button again, change the relationship type to No Relationship, click OK, then click the ... button again and redefine the relationship). If the red squiggly occurs on a linked measure group, you may need to delete that measure group and use the Linked Objects Wizard to recreate that linked measure group.

_Limitations:_
* DSV columns of type varchar(max) or nvarchar(max) are reported with a length of -1. If these columns have data over 4000 characters, you should manually fix the DataSize property on the KeyColumn or NameColumn properties. *{{site.title}}* will not do this for you. This scenario is described more fully [here](http://milambda.blogspot.com/2007/09/sql-server-2005-analysis-services.html).

_Tip:_ You can copy the data from the Dimension Data Type Discrepancy Check dialog with Ctrl-A then Ctrl-C and then paste it into Excel. If you feel the need to manually double check the changes *{{site.title}}* makes, this lets you copy and paste the list. The red coloring does not get copied to Excel, but red rows are generally rows where Old Data Type does not match New Data Type.

_Tip:_ After you refresh the DSV, run Dimension Data Type Discrepancy Check to quickly check whether any dimension attribute data types or lengths need to change.