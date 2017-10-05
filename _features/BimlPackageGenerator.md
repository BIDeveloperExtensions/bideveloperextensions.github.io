---
title: BIML Package Generator
component: ssis
---

The Biml Package Generator provides the ability to create packages from [Business Intelligence Markup Language (Biml)](http://www.varigence.com/Documentation/Language/Index). Biml is an XML-based language that allows you to describe your BI solution in a declarative fashion, similarly to using HTML to describe how a web page should appear. In addition, you can embed BimlScript (C# or VB.NET code) into Biml, in the same way that ASP.NET works with HTML. This allows for large numbers of packages to be created with a minimal amount of code.

For examples of using Biml, please see the [samples and tutorials ](-Samples-and-Tutorials) page.

To add a Biml file to the project, right-click on the project, or on the Data Sources, Data Source Views, or SSIS Packages folders. The context menu will have an **Add New Biml File** menu opton. This will add a Biml file to the Miscellaneous folder in the project.
![](Biml Package Generator_BimlPackageGenerator1.png)

Opening the Biml file will launch Visual Studio's XML editor, with Intellisense for the Biml language. If Intellisense is not working, see [Manually Configuring Biml Package Generator](Manually-Configuring-Biml-Package-Generator). To learn more about the Biml language, right-click on the .biml file and choose **Learn More About Biml** from the context menu. 
![](Biml Package Generator_BimlPackageGenerator2.png)

Here's a simple example of Biml code to create a package that contains a data flow:

```xml
<Biml xmlns="http://schemas.varigence.com/biml.xsd">
    <Packages>
        <Package Name="MyTestPackage" ConstraintMode="Linear" AutoCreateConfigurationsType="None">
            <Tasks>
                <Dataflow Name="My Data Flow">
                </Dataflow>
            </Tasks>
        </Package>
    </Packages>
</Biml>
```

After adding Biml code to a file, it can be checked for errors by choosing the **Check Biml for Errors** option from the context menu.

![](Biml Package Generator_BimlPackageGenerator3.png)

A Biml file can be expanded into one or more SSIS packages by choosing **Expand Biml File** from the menu. Expanding a file will automatically run an error check.

![](Biml Package Generator_BimlPackageGenerator4.png)

If the Biml file was expanded successfully, it will be added to the SSIS Packages folder in the project.

![](Biml Package Generator_BimlPackageGenerator5.png)

The Biml Package Generator is a plugin that leverages the Biml compiler from [Varigence](http://www.varigence.com). For more information on exactly what the free version of Biml in *{{site.title}}* supports, see the [Biml FAQ](/features/BimlFAQ/).