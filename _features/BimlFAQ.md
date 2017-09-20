---
title: "BIML: FAQ"
component: ssis
---

**Q: Why would I want to use Biml?**

**A:** Creating many similar Integration Services packages is a common task in ETL. Manually creating SSIS packages can consume a significant amount of time. And after you are done, if you decided you need to tweak your "template" to add in a new logging step or correct a bug, you will have to manually edit all the SSIS packages to manually add that change. A simple Biml script, on the other hand, can generate your SSIS packages for you and allow you to regenerate all your SSIS packages if you need to make a small change at a later date. For example, see [this example](Copy Data Dynamically with BimlScript) as an example of how a simple SQL metadata query and a loop can generate many SSIS packages dynamically.

**Q: How can I learn Biml?**

**A:** The [Samples and Tutorials](/features/SamplesandTutorials) page has many basic Biml examples to get you started. Additionally, the [BimlScript.com](http://BimlScript.com) website is another great resource. The support section of the [Varigence](http://varigence.com) site also has a User Guide, API & Language references and samples.

**Q: Is Biml inside *{{site.title}}* free?**

**A:** Yes, the version Biml inside *{{site.title}}* has been provided free of charge for *{{site.title}}* users. Any sources and destinations that come with the SSIS install itself are supported for free in *{{site.title}}* Biml. Other sources and destinations like the Attunity Oracle source and destination or the PDW destination which are installed "after market" may require the paid version of [Mist](https://www.varigence.com/Mist). For example, using the convenient [SqlServerPdwDestination tag](http://bimlscript.com/Snippet/Details/1124) requires Mist (as you will get a "No translator was found for the component <your component> of type AstSqlServerPdwDestinationNode in Dataflow <your data flow>" error in *{{site.title}}*), however you may be able to accomplish the same thing with the [much more complex CustomComponent tag](http://bimlscript.com/Walkthrough/Details/67) using the free version of Biml in *{{site.title}}*.

**Q: Is there a way to have Biml generate packages unattended during an automated nightly build?**

**A:** Biml inside *{{site.title}}* requires a user to start the Biml Package Generator. To automate SSIS package generation from Biml scripts unattended, you must purchase the paid version of [Mist](https://www.varigence.com/Mist) and use a command line tool called [Hadron.exe](http://www.varigence.com/Documentation/mist/Article/Hadron+Compiler+Command+Line+Options). Note Hadron is being renamed bimlc.exe as part of Mist 4.0.

**Q: I see some scripts on the internet mentioning Hadron but I don't see that in the Biml schema. What gives?**

**A:** The term Hadron is being renamed to Biml in *{{site.title}}* 1.7. For example, any code which reads:

``` xml
<#@ import namespace="Varigence.Hadron.CoreLowerer.SchemaManagement" #>
```

Should be changed to:

``` xml
<#@ import namespace="Varigence.Biml.CoreLowerer.SchemaManagement"  #>
```
**Q: Can I reverse engineer a working SSIS package to see the corresponding Biml?**

**A:** The paid version of [Mist](https://www.varigence.com/Mist) supports reverse engineering an SSIS package (.dtsx file) into a Biml script.

**Q: My BimlScript is not behaving like I expect. How can I debug it?**

**A:** Besides adding a code block to write to a log file, you can also add popups to your BimlScript expansion as described in this [blog post](http://www.bimlgeek.com/blog/popup-a-messagebox-within-bimlscript).

**Q: When I copy and paste into a .biml file in Visual Studio the script doesn't work and the indenting is all wrong. How can I fix this?**

**A:** The easiest way is to press Ctrl-V (to paste) and then Ctrl-Z (to undo indenting and formatting). This trick is further described and explained [here](http://bimlscript.com/Walkthrough/Details/45).