---
title: "BIML: Creating a basic package"
component: ssis
---


**Note: Varigence has stopped providing Biml for BI Developer Extensions so these features are deprecated. Instead install [BimlExpress](https://www.varigence.com/BimlExpress).**

--------------------

This article is going to walk through the process of creating a simple package using
[Biml](http://www.varigence.com/Documentation/Language/Index) and the [Biml Package Generator feature](/features/BimlPackageGenerator) in *{{site.title}}*. To start out, you need to install the [latest version](/downloads) of *{{site.title}}*. Once that is set up, you should create a new Integration Services project in BIDS. In the project, right-click on the Project in the Solution Explorer. There's a new item in this menu - Add New Biml File.

![](Creating a Basic Package Using Biml_image_2.png)

Clicking Add New Biml File will add a new file to the Miscellaneous folder in the solution named BimlScript.biml. (The name is automatically generated, so it may be BimlScript1.biml, etc). You can right-click on the file and choose rename to give the file a more specific name. For this example, rename the file "BasicPackage.biml".

Double-clicking on the file will open the XML editor inside of BIDS. The editor supports Intellisense for Biml, so typing an opening tag (&ldquo;&lt;&rdquo;) will give you a list of valid options for tags you can use. (If you aren't seeing the Intellisense, please [check this link for troubleshooting steps](/features/ManuallyConfiguringBimlPackageGenerator).)

![](Creating a Basic Package Using Biml_image_4.png)

For this example, copy and paste the following Biml into the document. Since the code below includes the document root tags (`<Biml>`), you'll want to make sure you replace the entire contents of the Biml file.

<pre>&lt;Biml xmlns=&quot;http://schemas.varigence.com/biml.xsd&quot;&gt;
    &lt;Connections&gt;
        &lt;Connection Name=&quot;AdventureWorks&quot; ConnectionString=&quot;Server=.;Initial Catalog=AdventureWorks;Integrated Security=SSPI;Provider=SQLNCLI10&quot;/&gt;
    &lt;/Connections&gt;
    &lt;Packages&gt;
        &lt;Package Name=&quot;Biml Sample&quot; AutoCreateConfigurationsType=&quot;None&quot; ConstraintMode=&quot;Linear&quot;&gt;
            &lt;Tasks&gt;
                &lt;Dataflow Name=&quot;Extract Table List&quot;&gt;
                    &lt;Transformations&gt;
                        &lt;OleDbSource Name=&quot;Get Table List&quot; ConnectionName=&quot;AdventureWorks&quot;&gt;
                            &lt;DirectInput&gt;SELECT * FROM sys.tables&lt;/DirectInput&gt;
                        &lt;/OleDbSource&gt;
                        &lt;Multicast Name=&quot;Multicast&quot;/&gt;
                    &lt;/Transformations&gt;
                &lt;/Dataflow&gt;
            &lt;/Tasks&gt;
        &lt;/Package&gt;
    &lt;/Packages&gt;
&lt;/Biml&gt;</pre>

The first section (`<Connections>`) of this Biml defines an OleDbConnection that points to the AdventureWorks database. The next section (inside the `<Packages>` tag) defines a single package that contains a Dataflow task (the `<Dataflow>` tag).

The Dataflow task contains two components, an OleDb Source and an Union All transformation.

The next step is to take this definition of a package, and actually generate the package from it. To do this, right-click on the Biml file, and choose Expand Biml File from the context menu.

![](Creating a Basic Package Using Biml_image_6.png)


(In later versions of *{{site.title}}*, the option is called "Generate SSIS Packages".)

A new package will be added to the SSIS Packages folder, named Biml Sample.dtsx. If you review the generated package, you'll see that it matches up to what was defined in the Biml code.

![](Creating a Basic Package Using Biml_image_12.png)![](Creating a Basic Package Using Biml_image_14.png)

That's a quick introduction to the Biml functionality in *{{site.title}}*. In the next article, we'll set the stage for some more advanced (read: more interesting) uses of Biml, including some scripting.

\[cross posted from [http://agilebi.com/jwelch/2011/05/13/creating-a-basic-package-using-biml/](http://agilebi.com/jwelch/2011/05/13/creating-a-basic-package-using-biml)]