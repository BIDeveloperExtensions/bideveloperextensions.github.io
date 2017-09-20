---
title: Pipeline Component Performance Breakdown
category: ssis
component: ssis
---

In SSIS2005, it is very difficult to determine which piece of a data flow task is the bottleneck. There are recommended instructions for [measuring performance](http://www.microsoft.com/technet/prodtechnol/sql/2005/ssisperf.mspx#EYKAC) of the components in the data flow, but this methodology can be very tedious to step through manually. *{{site.title}}*'s Pipeline Component Performance Breakdown feature automates this methodology for you and lets you trend component performance as you try different settings and design alternatives.

(In SSIS2008, look at the built-in PipelineComponentTime event.)

To launch this feature, right click on a Data Flow task on the control flow tab of the SSIS package designer and choose "Performance Breakdown". (You can also launch this feature by right clicking on the background of the data flow tab's design surface and choosing the same menu option.)

![](Pipeline Component Performance Breakdown_BreakdownControlFlowMenu.png)

*{{site.title}}* makes a temporary copy of your package, pulls it apart into a number of testing iterations to measure and isolate component performance, then reports the individual durations of each component.

In the following example, the Trial 1 column represents the first time I ran this feature. Previously, I couldn't tell whether the source, the lookup, or the destination was the bottleneck, but the grid clearly shows the Lookup is the bottleneck. Upon closer examination, I noticed I had enabled memory restriction for that lookup component causing SSIS to execute singleton SQL queries, one per row in the pipeline, to perform the lookup. I disabled memory restriction which caused the lookup table to be cached in memory once, and performance was drastically improved, as seen in the Trial 2 column.

![](Pipeline Component Performance Breakdown_BreakdownSlowLookup.png)

As the tests are being run, the source components pumped to raw files so that each source is only hit once. Also, the data is only pumped to the destinations once per execution of this feature.


**Testing Methodology Example**

When the temp package is broken apart into separate test iterations utilizing raw files and rowcount transforms as replacements, a very simple package would be tested in the following way:

![](Pipeline Component Performance Breakdown_BreakdownTestMethodology.png)

1. The original data flow. The full data flow is never run as part of the Pipeline Component Performance Breakdown feature.
1. Isolate the source and write it to a raw file so that it will never have to be queried again. The raw file is written to a temp directory on your system drive (usually the C drive).
1. Isolate each transform component one at a time. Sources are replaced with raw file sources. Everything downstream is removed and replaced with a rowcount transform.
1. After all transforms are tested, the final output to the destination is written to a raw file. This raw file will be used in test 5 to isolate the destination time. This execution duration is not reported.
1. Isolate the destination and pump a raw file directly to it. Destinations are written to only once.

**Errors:** If any errors occur during one of the test iterations, *{{site.title}}* stops and asks you if you would like to troubleshoot the temp copy of the packages. If you accept, it will not delete the temp directory so that you can troubleshoot the error. Please report any problemmatic packages to the [issue tracker](/issues).


**Cavaets:**
* If any TEXT, NTEXT, or IMAGE columns are used in the pipeline, that section of the pipeline will not be able to use raw files, since these datatypes are not supported in raw files. In such cases, the source component may be queried during each test iteration instead of just once as described above.
* Everything else but the data flow task you're testing is removed from the temporary copy of the package.
	* Therefore, you should manually run (by right clicking on the tasks and selecting Execute Task) any other prerequisite tasks (which truncate destinations tables, for example).
	* Also, the data flow task you are testing is moved to the package surface itself (so it is no longer in any for loops or sequence containers). Therefore, any package configurations that were directly setting data flow task properties will be skipped during execution of this *{{site.title}}* feature. Package configurations operating on other package objects such as connection managers will still take effect.
* The test iterations are executed using the same code as [SSIS Performance Visualization](../SSISPerformanceVisualization) uses. So note everything relevant on that page such as 64-bit dtexec, your SSIS logging being disabled, etc.