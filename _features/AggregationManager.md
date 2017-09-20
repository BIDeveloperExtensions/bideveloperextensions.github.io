---
title:  Aggregation Manager
category: ssas
component: ssasm
---

Microsoft provides an [Aggregation Manager](http://www.codeplex.com/MSFTASProdSamples/Wiki/View.aspx?title=SS2005%21Readme%20for%20Aggregation%20Manager%20Sample&referringTitle=Home) sample application which gives an advanced interface for manually editing aggregations. We have taken this sample code and integrated it into *{{site.title}}*. This way, it can be run from Visual Studio when you're designing your cube, and aggregations you edit will be saved into your source code for the cube. (If you prefer, you can run the *{{site.title}}* version of Aggregation Manager live against a deployed cube if you open it through File... Open... Analysis Services Database.)

A number of bug fixes and enhancements were coded. Look at the [complete list](http://www.codeplex.com/MSFTASProdSamples/WorkItem/View.aspx?WorkItemId=268) if you're interested. It also contains a few completely new features: [Delete Unused Aggregations](../DeleteUnusedAggregations), [Validate Aggregations](../ValidateAggregations), [Printer Friendly Aggregations](../PrinterFriendlyAggregations), and [Similar Aggregations](../SimilarAggregations).

To use Aggregation Manager, right click on the cube in Solution Explorer:

![](Aggregation Manager_AggManagerTeaser.gif)

Then you are given windows which allow you to edit aggregations manually:

![](Aggregation Manager_AggsEditorWindow.png)

Appendix C of the [performance guide](http://download.microsoft.com/download/8/5/e/85eea4fa-b3bb-4426-97d0-7f7151b2011c/SSAS2005PerfGuide.doc) provides documentation on how to use Aggregation Manager. The UI of Aggregation Manager inside {{site.ms-designer}} is only slightly different in a few places.

Aggregation Manager can also be launched from the Partition tab of the cube designer:
![](Aggregation Manager_EditAggsButton.png)

After completing your edits to aggregations using Aggregation Manager, you can deploy your changes using the [Deploy Aggregation Designs](../DeployAggregationDesigns) feature. That feature will deploy all changes made in Aggregation Manager except the assignment of aggregation designs to particular partitions.

The instantaneous aggregation size estimate (which shows at the top of the screen) does as good a job as is possible estimating the size based upon the EstimatedCount of dimension attributes, the EstimatedRows of the measure group, and the number of dimension keys included in the aggregation. (If the EstimatedCount/EstimatedRows properties are not set or are not up to date, then use the [Update Estimated Counts](../UpdateEstimatedCounts) feature.) When it shows a range of estimated sizes, the uncertainty is due to the unknown sparsity when you crossjoin multiple dimensions. For exact aggregation sizes, deploy the aggregation design, run ProcessIndex, then use the Physical Aggregation Sizes screen which can be opened via the context menu of an individual partition in Agg Manager.