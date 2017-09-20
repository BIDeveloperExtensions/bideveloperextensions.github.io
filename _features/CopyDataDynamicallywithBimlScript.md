---
title: "BIML: Copy Data Dynamically with BimlScript"
component: ssis
---

*This post is [part 3 of a series](http://agilebi.com/jwelch/2011/05/13/biml-functionality-in-bids-helper/) on using
[Biml](http://www.varigence.com/documentation/biml/) in {{site.title}}. This post builds on some of the information and the sample from the previous posts.*

BimlScript enables some interesting scenarios for generating large numbers of SSIS packages automatically. This can come in handy when you need to copy most or all of the data in one database to a different one. In this case, you could use something like the [Transfer SQL Server Objects](http://msdn.microsoft.com/en-us/library/ms142159.aspx) task, but [it has a few problems](http://blogs.msdn.com/b/mattm/archive/2007/04/18/roll-your-own-transfer-sql-server-objects-task.aspx). You can roll your own, but that might mean a fair amount of custom scripting. Or you could use the Import / Export Wizard. But in all these cases, you don&rsquo;t have complete control of how the packages are produced. You could create all the packages by hand, which does give you full control, but then you are stuck doing a lot of repetitive work in SSIS.

BimlScript provides an alternative that lets you fully control the output, while automating the rote work of producing lots of packages that use the same pattern. Let&rsquo;s take a look at a sample of this, using the scenario above (copying the data from one database to another).

<pre>&lt;#@ template language=&quot;C#&quot; hostspecific=&quot;true&quot;#&gt;
&lt;#@ import namespace=&quot;System.Data&quot; #&gt;
      
&lt;Biml xmlns=&quot;http://schemas.varigence.com/biml.xsd&quot;&gt;
      &lt;Connections&gt;
            &lt;OleDbConnection Name=&quot;Source&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=SSPI;&quot;/&gt;
            &lt;OleDbConnection Name=&quot;Target&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=Target;Integrated Security=SSPI;&quot;/&gt;
      &lt;/Connections&gt;
      &lt;Packages&gt;
            &lt;# 
                string metadataConnectionString = &quot;Provider=SQLNCLI10;Server=.;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=SSPI;&quot;;
                DataTable tables = ExternalDataAccess.GetDataTable(metadataConnectionString, 
                    &quot;SELECT '[' &#43; s.name &#43; '].[' &#43; t.name &#43; ']' FROM sys.tables t INNER JOIN sys.schemas s on t.schema_id = s.schema_id&quot;);
                foreach (DataRow row in tables.Rows)
                { #&gt;
            &lt;Package Name=&quot;Extract &lt;#=row[0]#&gt;&quot; ConstraintMode=&quot;Linear&quot; AutoCreateConfigurationsType=&quot;None&quot;&gt;
                  &lt;Tasks&gt;
                        &lt;Dataflow Name=&quot;Copy Data&quot;&gt; 
                              &lt;Transformations&gt;
                                    &lt;OleDbSource Name=&quot;Retrieve Data&quot; ConnectionName=&quot;Source&quot;&gt;
                                          &lt;DirectInput&gt;SELECT * FROM &lt;#=row[0]#&gt;&lt;/DirectInput&gt;
                                    &lt;/OleDbSource&gt;
                                    &lt;OleDbDestination Name=&quot;Insert Data&quot; ConnectionName=&quot;Target&quot;&gt;
                                          &lt;ExternalTableOutput Table=&quot;&lt;#=row[0]#&gt;&quot;/&gt;
                                    &lt;/OleDbDestination&gt;
                              &lt;/Transformations&gt;
                        &lt;/Dataflow&gt;
                  &lt;/Tasks&gt;
            &lt;/Package&gt;
                &lt;# } #&gt;
      &lt;/Packages&gt;
&lt;/Biml&gt;</pre>

>Note: When you paste this into Visual Studio, the formatting and indenting will be wrong and the code will not work. After pasting, press Ctrl-Z to undo formatting and indenting and the paste will be successful. See [this
 tip](http://bimlscript.com/Walkthrough/Details/45) for more information.

This script is set up to copy all the data in the AdventureWorksDW2008R2 database to a second database named Target (very inventive, I know). One note - the script is not creating the tables in the target database. We could actually automate that portion as well, but it's beyond the scope of this post. To ensure you are set up properly to run this script, you should create an exact structural copy of your source database under a different name. You can use the [Generate Scripts Wizard](http://msdn.microsoft.com/en-us/library/ms178078(v=SQL.105)) to do this. Just script the entire database, and then update the generated script to use a different database name (don't forget to change the USE statement to the new name).

The script will produce a package per table, with a simple data flow that copies all the data using an OLE DB Source and OLE DB Destination. The script leverages the metadata already contained in the database, in the sys.tables view, to drive the loop that creates the packages.

What if you don't want to select all the rows from each table? Instead, perhaps you want to specify a WHERE clause to use to filter some of the tables. To handle this, we can create a table in the target database that holds our WHERE information.

<pre>&lt;Biml xmlns=&quot;http://schemas.varigence.com/biml.xsd&quot;&gt;
    &lt;Connections&gt;
        &lt;OleDbConnection Name=&quot;Target&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=Target;Integrated Security=SSPI;&quot;/&gt;
    &lt;/Connections&gt;
    &lt;Tables&gt;
        &lt;Table Name=&quot;WhereClause&quot; ConnectionName=&quot;Target&quot;&gt;
            &lt;Columns&gt;
                &lt;Column Name=&quot;TableName&quot; DataType=&quot;String&quot; Length=&quot;255&quot;/&gt;
                &lt;Column Name=&quot;WhereSql&quot; DataType=&quot;String&quot; Length=&quot;4000&quot;/&gt;
            &lt;/Columns&gt;
        &lt;/Table&gt;
    &lt;/Tables&gt;
&lt;/Biml&gt;</pre>

<p>You can use the <a href="http://agilebi.com/jwelch/2011/05/26/creating-tables-using-biml-and-bimlscript/">
steps shown in Part 2 of this series</a> to create this table in the Target database. Once it&rsquo;s been created, populate it with some data. Note that since we are using the schema-qualified name of the table, you&rsquo;ll need to specify that in the table.
 There&rsquo;s an example of data for this table that will work with AdventureWorksDW2008R2 below. This will filter the rows down to only sales where the amount is greater than 1000.</p>

<table border="1" width="610" cellspacing="0" cellpadding="2">
<tbody>
<tr>
<td valign="top" width="200"><strong><span style="font-size:small">TableName</span></strong></td>
<td valign="top" width="408"><strong><span style="font-size:small">SelectSql</span></strong></td>
</tr>
<tr>
<td valign="top" width="200">[dbo].[FactInternetSales]</td>
<td valign="top" width="408">
<pre>WHERE [SalesAmount] &gt;= 1000</pre>
</td>
</tr>
<tr>
<td valign="top" width="200">[dbo].[FactResellerSales]</td>
<td valign="top" width="408">
<pre>WHERE [SalesAmount] &gt;= 1000</pre>
</td>
</tr>
</tbody>
</table>

Now we need to alter the script to use the new information in this table. At the beginning of the block of script after the `<Packages>` element, add the following code:

<pre>string targetConnectionString = &quot;Provider=SQLNCLI10;Server=.;Initial Catalog=Target;Integrated Security=SSPI;&quot;;
DataTable whereClauses = ExternalDataAccess.GetDataTable(targetConnectionString, &quot;SELECT TableName, WhereSql FROM WhereClause&quot;);
</pre>

This retrieves the WHERE clauses from the WhereClause table, and stores them in the whereClauses variable.

Next, replace the `<Direct Input>` line in the OleDbSource with this:

<pre>&lt;# 
  var dataRow = whereClauses.Select(string.Format(&quot;TableName = '{0}'&quot;, row[0]));
  string whereSql = dataRow.Length == 0 ? string.Empty : dataRow[0][1].ToString();    
  string sql = string.Format(&quot;SELECT * FROM {0} {1}&quot;, row[0], whereSql);
#&gt;
&lt;DirectInput&gt;&lt;#=sql#&gt;&lt;/DirectInput&gt;</pre>

This code determines whether the whereClauses table has a row for the current table. If it does, it appends it to the end of the SELECT statement. The complete, final script looks like this:

<pre>&lt;#@ template language=&quot;C#&quot; hostspecific=&quot;true&quot;#&gt;
&lt;#@ import namespace=&quot;System.Data&quot; #&gt;
      
&lt;Biml xmlns=&quot;http://schemas.varigence.com/biml.xsd&quot;&gt;
      &lt;Connections&gt;
            &lt;OleDbConnection Name=&quot;Source&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=SSPI;&quot;/&gt;
            &lt;OleDbConnection Name=&quot;Target&quot; ConnectionString=&quot;Provider=SQLNCLI10;Server=.;Initial Catalog=Target;Integrated Security=SSPI;&quot;/&gt;
      &lt;/Connections&gt;
      &lt;Packages&gt;
            &lt;# 
                string targetConnectionString = &quot;Provider=SQLNCLI10;Server=.;Initial Catalog=Target;Integrated Security=SSPI;&quot;;
                DataTable whereClauses = ExternalDataAccess.GetDataTable(targetConnectionString, &quot;SELECT TableName, WhereSql FROM WhereClause&quot;);
                
                string metadataConnectionString = &quot;Provider=SQLNCLI10;Server=.;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=SSPI;&quot;;
                DataTable tables = ExternalDataAccess.GetDataTable(metadataConnectionString, 
                    &quot;SELECT '[' &#43; s.name &#43; '].[' &#43; t.name &#43; ']' FROM sys.tables t INNER JOIN sys.schemas s on t.schema_id = s.schema_id&quot;);
                foreach (DataRow row in tables.Rows)
                { #&gt;
            &lt;Package Name=&quot;Extract &lt;#=row[0]#&gt;&quot; ConstraintMode=&quot;Linear&quot; AutoCreateConfigurationsType=&quot;None&quot;&gt;
                  &lt;Tasks&gt;
                        &lt;Dataflow Name=&quot;Copy Data&quot;&gt; 
                              &lt;Transformations&gt;
                                    &lt;OleDbSource Name=&quot;Retrieve Data&quot; ConnectionName=&quot;Source&quot;&gt;
                                        &lt;# 
                                            var dataRow = whereClauses.Select(string.Format(&quot;TableName = '{0}'&quot;, row[0]));
                                            string whereSql = dataRow.Length == 0 ? string.Empty : dataRow[0][1].ToString();    
                                            string sql = string.Format(&quot;SELECT * FROM {0} {1}&quot;, row[0], whereSql);
                                        #&gt;
                                          &lt;DirectInput&gt;&lt;#=sql#&gt;&lt;/DirectInput&gt;
                                    &lt;/OleDbSource&gt;
                                    &lt;OleDbDestination Name=&quot;Insert Data&quot; ConnectionName=&quot;Target&quot;&gt;
                                          &lt;ExternalTableOutput Table=&quot;&lt;#=row[0]#&gt;&quot;/&gt;
                                    &lt;/OleDbDestination&gt;
                              &lt;/Transformations&gt;
                        &lt;/Dataflow&gt;
                  &lt;/Tasks&gt;
            &lt;/Package&gt;
                &lt;# } #&gt;
      &lt;/Packages&gt;
&lt;/Biml&gt;</pre>

You can see the results of this script by <a href="http://agilebi.com/jwelch/2011/05/13/creating-a-basic-package-using-biml/">
right-clicking on the Biml file, and choosing Expand</a>. It may take a minute or two to process, but when it finishes, you should see a package for each table in your source database. The data flows will copy the data from Source to Target, and any WHERE clauses
 you add to the WhereClause table will be used.

There's a lot more that could be done with this script (automating the recreation of the tables in the destination, or deleting existing data, for example), but it&rsquo;s still a good example of what BimlScript can do. Instead of spending your time writing 10s or 100s of repetitive packages, automate it with BimlScript.

<p>[cross-posted from <a title="http://agilebi.com/jwelch/2011/05/31/copy-data-dynamically-with-bimlscript/" href="http://agilebi.com/jwelch/2011/05/31/copy-data-dynamically-with-bimlscript/">
http://agilebi.com/jwelch/2011/05/31/copy-data-dynamically-with-bimlscript/</a>]</p>
