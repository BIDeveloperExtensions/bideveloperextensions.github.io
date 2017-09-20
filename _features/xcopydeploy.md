---
title: X-copy Deployment
component: common
---
To do an "xcopy deploy" you simply download the zip file for for your version of SQL Server (instead of the setup .exe) and unzip the  zip file to either:

<My Documents>/Visual Studio 2005/Addins  _(for SQL Server 2005)_
_or_
<My Documents>/Visual Studio 2008/Addins  _(for SQL Server 2008 and SQL Server 2008 R2)_
_or_
<My Documents>/Visual Studio 2010/Addins  _(for SQL Server 2012 in Visual Studio 2010)_
_or_
<My Documents>/Visual Studio 2012/Addins  _(for SQL Server 2012 in Visual Studio 2012)_
_or_
<My Documents>/Visual Studio 2013/Addins  _(for SQL Server 2014 in Visual Studio 2013)_

If the Addins directory doesn't exist already, create it.

This lets your run *{{site.title}}* in situations where you do not have administrator rights on the machine in order to be able to run the full installer.

For SQL Server 2012 and SQL Server 2014, you must also unblock every file in the Addins directory:

![](xcopy deploy_unblock.png)

(If you don't unblock the DLLs, you will get the error message: "The Add-in 'BIDSHelper' failed to load or caused an exception. Error number: 80131515")

After restarting Visual Studio, check Help... About Microsoft Visual Studio and make sure you see *{{site.title}}*. If you don't, you may need to go to Tools... Options... Add-in/Macro Security... then add the above path to the list, then restart Visual Studio. If you see *{{site.title}}* but it is not functioning, look at the [Tools... Options... *{{site.title}}*... Version](Version-Notification) tab for more information about the problem.

To fully configure the [Biml Package Generator](Biml-Package-Generator) plugin as part of an xcopy deployment, please see [Manually Configuring Biml Package Generator](Manually-Configuring-Biml-Package-Generator).