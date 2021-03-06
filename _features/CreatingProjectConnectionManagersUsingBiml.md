---
title: "BIML: Creating Project Connection Managers"
component: ssis
---


**Note: Varigence has stopped providing Biml for BI Developer Extensions so these features are deprecated. Instead install [BimlExpress](https://www.varigence.com/BimlExpress).**

--------------------

This article is going to walk through the process of creating an SSIS 2012 package which uses a project connection manager using
<a href="http://www.varigence.com/documentation/biml/">Biml</a> and the [Biml Package Generator feature](/features/BimlPackageGenerator) in *{{site.title}}*.

This feature is available in *{{site.title}}* 1.6.3 and later and in SSIS 2012 projects in project deployment mode (not in legacy deployment mode). The code for this feature was generously created for the community by
<a href="http://www.davidemauri.it/">Davide Mauri</a>.


For this example, copy and paste the following Biml into the a .biml document, as seen in the other examples.

<pre>&lt;Biml xmlns=&quot;http://schemas.varigence.com/biml.xsd&quot;&gt;<br>&nbsp; &lt;Connections&gt;<br>&nbsp;&nbsp;&nbsp; &lt;OleDbConnection Name=&quot;OLTP&quot; ConnectionString=&quot;Data Source=localhost;Initial Catalog=tempdb;Provider=SQLNCLI11.1;Integrated Security=SSPI;Auto Translate=False;&quot; <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CreateInProject=&quot;false&quot;/&gt;<br>&nbsp;&nbsp;&nbsp; &lt;OleDbConnection Name=&quot;OLTP2&quot; ConnectionString=&quot;Data Source=localhost;Initial Catalog=tempdb;Provider=SQLNCLI11.1;Integrated Security=SSPI;Auto Translate=False;&quot; <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ff0000">CreateInProject=&quot;true&quot;</span>/&gt;<br>&nbsp; &lt;/Connections&gt;<br>&nbsp; &lt;Packages&gt;<br>&nbsp;&nbsp;&nbsp; &lt;Package Name=&quot;Test2&quot; ConstraintMode=&quot;Linear&quot;&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Connections&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Connection ConnectionName=&quot;OLTP2&quot;/&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Connections&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Tasks&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ExecuteSQL Name=&quot;ES Test A&quot; ConnectionName=&quot;OLTP2&quot;&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;DirectInput&gt;SELECT Test=1;&lt;/DirectInput&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/ExecuteSQL&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ExecuteSQL Name=&quot;ES Test B&quot; ConnectionName=&quot;OLTP&quot;&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;DirectInput&gt;SELECT Test=1;&lt;/DirectInput&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/ExecuteSQL&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Dataflow Name=&quot;DF Test&quot;&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Transformations&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;OleDbSource ConnectionName=&quot;OLTP2&quot; Name=&quot;Source&quot;&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;DirectInput&gt;SELECT Test=1;&lt;/DirectInput&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/OleDbSource&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;OleDbDestination ConnectionName=&quot;OLTP&quot; Name=&quot;Dest&quot;&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ExternalTableOutput Table=&quot;dbo.Dest&quot;&gt;&lt;/ExternalTableOutput&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/OleDbDestination&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Transformations&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Dataflow&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Tasks&gt;<br>&nbsp;&nbsp;&nbsp; &lt;/Package&gt;<br>&nbsp; &lt;/Packages&gt;<br>&lt;/Biml&gt;</pre>

Note the CreateInProject='true' setting in red on the connection. This signals Biml to create a project level connection manager.

