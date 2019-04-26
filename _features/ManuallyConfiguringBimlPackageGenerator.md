---
title: "BIML: Manually Configuring BIML Package Generator"
component: ssis
---


**Note: Varigence has stopped providing Biml for BI Developer Extensions so these features are deprecated. Instead install [BimlExpress](https://www.varigence.com/BimlExpress).**

--------------------

If you are doing an xcopy deployment of *{{site.title}}*, or experience any issues with the Biml Package Generator, please review the items on this page to make sure your environment is configured for the best experience. None of these are required to use the Biml Package Generator, but they make it more enjoyable.

The simplest option is to make sure that `Biml.xsd` has been copied to the Visual Studio registered schemas folder. This will enable Intellisense when working with Biml files in {{site.ms-designer}}. The following tables shows the location of schemas folder for each version of Visual Studio.

|Version|Folder|
|-------|------|
|2005|C:\Program Files (x86)\Microsoft Visual Studio 8\Xml\Schemas|
|2008|C:\Program Files (x86)\Microsoft Visual Studio 9.0\Xml\Schemas|
|2010|C:\Program Files (x86)\Microsoft Visual Studio 10.0\Xml\Schemas|
|2012|C:\Program Files (x86)\Microsoft Visual Studio 11.0\Xml\Schemas|
|2013|C:\Program Files (x86)\Microsoft Visual Studio 12.0\Xml\Schemas|

If you are running on a 32-bit operating system, your folders will start `C:\Program Files\` instead of `C:\Program Files (x86)\`.

Alternatively if you don't want to copy `Biml.xsd` to the schemas directory, you can manually associate it with a Biml file in the Visual Studio environment. To do this, open the Biml file in {{site.ms-designer}}, and then open the Properties window (F4 is the default shortcut). Select the Schemas property, and click the ellipsis button to browse to your location for `Biml.xsd`. If you take this approach, you will have to re-associate the .xsd each time you open a Biml file.