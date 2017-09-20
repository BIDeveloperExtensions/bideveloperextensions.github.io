---
title: Update Estimated Counts
category: ssas
component: ssasm
---

This feature allows you to update the EstimatedCount property of every dimension attribute and every partition with exact counts. Better counts help the Aggregation Design Wizard choose better aggregations.

This feature comes in handy when the estimated counts get out of date and you want to redesign aggregations. The Aggregation Design Wizard has a screen to edit counts, but updating existing counts requires zeroing out incorrect ones manually.

Note that this feature can be _incredibly_ slow if partitions or dimensions have millions of rows or are based upon expensive queries, and once the counting is running it should not be cancelled or some counts may be left at zero.

This feature can be launched from the Partition tab of the cube designer:

![](Update Estimated Counts_EstimatedCountsTeaser.png)

Once running, you can cancel (not recommended) this counting operation by clicking the stop button which appears:

![](Update Estimated Counts_CancelEstimatedCounts.png)