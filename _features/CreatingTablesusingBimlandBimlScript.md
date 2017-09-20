---
title: "BIML: Creating tables using BIML and BIMLScript"
component: ssis
---

*This post is [part 2 of a series](http://agilebi.com/jwelch/2011/05/13/biml-functionality-in-bids-helper/) on using [Biml](http://www.varigence.com/Documentation/Language/Index) in *{{site.title}}*. This post builds on some of the information and the sample from the previous posts.

When I'm creating samples for SSIS, I often find it necessary to create supporting tables to go along with the package sample. One of the things I like about [Biml](http://www.varigence.com/Documentation/Language/Index) is that you can define both your tables and packages in the language. Here's an example of defining an OrderHeader and OrderDetail table in Biml:

``` xml
<Biml xmlns="http://schemas.varigence.com/biml.xsd">
  <Connections>
    <OleDbConnection Name="DbConnection" ConnectionString="Server=.;Initial Catalog=tempdb;Provider=SQLNCLI10.1;Integrated Security=SSPI;"/>
  </Connections>
  <Databases>
    <Database ConnectionName="DbConnection" Name="tempdb"/>
  </Databases>
  <Schemas>
    <Schema Name="dbo" DatabaseName="tempdb" Owner="dbo"/>
  </Schemas>
  <Tables>
    <Table Name="OrderHeader" SchemaName="tempdb.dbo">
      <Columns>
        <Column Name="OrderId" DataType="Int32" IdentityIncrement="1" IdentitySeed="1"/>
        <Column Name="SalesDate" DataType="DateTime"/>
        <Column Name="CustomerName" DataType="String" Length="50"/>
      </Columns>
      <Keys>
        <PrimaryKey Name="OrderHeaderPK">
          <Columns>
            <Column ColumnName="OrderId"/>
          </Columns>
        </PrimaryKey>
      </Keys>
    </Table>
    <Table Name="OrderDetail" SchemaName="tempdb.dbo">
      <Columns>
        <Column Name="OrderDetailId" DataType="Int32" IdentityIncrement="1" IdentitySeed="1"/>
        <TableReference Name="OrderId" TableName="OrderHeader"/>
        <Column Name="ProductName" DataType="String" Length="50"/>
        <Column Name="Qty" DataType="Int16"/>
        <Column Name="UnitPrice" DataType="Currency"/>
      </Columns>
      <Keys>
        <PrimaryKey Name="OrderDetailPK">
          <Columns>
            <Column ColumnName="OrderDetailId"/>
          </Columns>
        </PrimaryKey>
      </Keys>
    </Table>
  </Tables>
</Biml>
```


Tables are defined in a <[Table](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Table.AstTableNode.html)> tag. They can have columns defined, as well as keys, and even indexes (not shown in the example above). Notice that the OrderId column doesn&rsquo;t have a DataType attribute. Many of the attributes in Biml have default values, and data type is one of them. If it's not specified, the column data type will default to Int32. The primary key for the table is defined with a <[PrimaryKey](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Table.AstTablePrimaryKeyNode.html)> element.

The OrderDetail table includes a <[TableReference](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Table.AstTableColumnTableReferenceNode.html)> column. TableReference columns are a special class of columns, that define that this column should have a foreign key reference to another table. This one is referencing back to the OrderHeader table. It's not shown, but you can also use a 
[MultipleColumnTableReference](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Table.AstMultipleColumnTableReferenceNode.html), if your foreign key needs to span multiple columns.

Great - now you have your tables defined in Biml, but how do you make use of that? If only there were some way to run this against your database to create the tables... Well, fortunately, there is - by using BimlScript. BimlScript is a scripting layer that automates the production of Biml (similar in concept to the way ASP.NET produces HTML). To set this up, you need to add two Biml files to your project - one to hold the table definitions above, and one to hold the BimlScript.

First, add a new Biml file to the SSIS project (see [Part 1](http://agilebi.com/jwelch/2011/05/13/creating-a-basic-package-using-biml/) if you need a refresher on this). Copy the Biml above to this file, and rename the file to TableDefinitions.biml.

![](Creating Tables using Biml and BimlScript_image_2.png)

Second, add an additional Biml file. Name this one CreateTables.biml.

![](Creating Tables using Biml and BimlScript_image_4.png)

Open the CreateTables.biml file, and replace the contents with the following code:

``` xml
<#@ template language="C#" hostspecific="True" #>
<Biml xmlns="http://schemas.varigence.com/biml.xsd">
  <Packages>
    <Package Name="Create Tables" AutoCreateConfigurationsType="None" ConstraintMode="Linear">
      <Tasks>
        <# foreach(var table in RootNode.Tables) {#>
        <ExecuteSQL Name="Create <#=table.Name#>" ConnectionName="<#=table.Connection.Name#>">
          <DirectInput>
              <#=table.GetTableSql()#>    
          </DirectInput>
        </ExecuteSQL>
        <# } #>
      </Tasks>
    </Package>
  </Packages>
</Biml>
```

*Note:* When you paste this into Visual Studio, the formatting and indenting will be wrong and the code will not work.&nbsp;After pasting, press Ctrl-Z to undo formatting and indenting and the paste will be successful. See [this tip](http://bimlscript.com/Walkthrough/Details/45) for more information.

This file has a header at the beginning that indicates the script will use C#. The next section defines a package named "Create Tables". The RootNode.Tables section inside the Tasks element is the interesting part.&nbsp;This code iterates over the tables that are part of the current model. For each table it finds, it creates an ExecuteSQL task, and embeds the SQL to create the table in the package. The code could be repeated to iterate over
[Dimensions](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Dimension.AstDimensionNode.html) and [Facts](http://www.varigence.com/documentation/biml/biml_Varigence.Languages.Biml.Fact.AstFactNode.html), which are special classes of tables.

Notice that there are no tables defined in the BimlScript file. The BimlScript can't operate against objects defined in the same file, which is why we created the TableDefinitions.biml file separately. To produce the package, multi-select both TableDefinitions.biml, and CreateTables.biml, right-click, and choose Expand Biml File.

![](Creating Tables using Biml and BimlScript_image_6.png)

This will produce a new SSIS package in the project named Create Tables.dtsx. It contains two Execute SQL tasks, one for each table.

![](Creating Tables using Biml and BimlScript_image_8.png)

Each task includes the appropriate SQL to create the tables. As an example, here's the OrderHeader SQL from the Execute SQL task.

``` SQL
SET ANSI_NULLS ON
SET QUOTED_IDENTIFIER ON
GO

-------------------------------------------------------------------
IF EXISTS (SELECT * from sys.objects WHERE object_id = OBJECT_ID(N'[OrderHeader]') AND type IN (N'U'))
DROP TABLE [OrderHeader]
GO

CREATE TABLE [OrderHeader]
(
-- Columns Definition
 [OrderId] int IDENTITY(1,1) NOT NULL
, [SalesDate] datetime NOT NULL
, [CustomerName] nvarchar(50) NOT NULL

-- Constraints
,CONSTRAINT [OrderHeaderPK] PRIMARY KEY CLUSTERED
(
  [OrderId] Asc) WITH(PAD_INDEX = OFF,IGNORE_DUP_KEY = OFF) ON [PRIMARY]

)
ON [PRIMARY]
WITH (DATA_COMPRESSION = NONE)
GO

-------------------------------------------------------------------
```
Note that the tables are ordered in the package in the same order they are defined in the Biml file. If you have tables with dependencies, make sure to order them correctly.

In the next post, we'll look at some ways to copy data dynamically using BimlScript.

\[cross-posted with updates from [http://agilebi.com/jwelch/2011/05/26/creating-tables-using-biml-and-bimlscript/](http://agilebi.com/jwelch/2011/05/26/creating-tables-using-biml-and-bimlscript/)]