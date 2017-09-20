---
title: Validate Aggregations
category: ssas
component: ssasm
---
The Validate Aggregations feature allows you to quickly check whether any aggregations violate restrictions or best practices. It can be launched from the Aggregation Editor window from [Aggregation Manager](../AggregationManager):

![](Validate Aggregations_ValidateAggsButton.png)

It can also be launched for the entire cube from the main Aggregation Manager window:

![](Validate Aggregations_ValidateAggsCubeMenu.png)

Currently, the following rules and best practices are checked:

1. Any aggregation intended to improve performance of a many-to-many dimension must include the granularity attribute of all dimensions in common with the intermediate measure group. (For instance, if you build an agg on the Internet Sales measure group to optimize the Sales Reason many-to-many dimension, the agg must also include the Internet Sales Order attribute of the Internet Sales Order Details dimension.) Also, the many-to-many dimension itself should not be included in the aggregation to workaround a [bug](https://connect.microsoft.com/SQLServer/feedback/ViewFeedback.aspx?FeedbackID=303448).
1. Aggregations designed to optimize semi-additive measures must include the granularity of the Time dimension. Therefore, a warning is issued if the measure group has only semi-additive measures and an aggregation does not include Time dimension granularity.
1. No aggregation can include an attribute from a non-materialized reference dimension as this will not return correct numbers at query time.
1. No aggregation can include a parent-child attribute as this is not supported by Analysis Services. The key attribute of the dimension should be included instead.
1. No aggregation can include an attribute which is marked with AttributeHierarchyEnabled=false.
1. Any attributes which have a DefaultMember, which are not aggregatable, or which are marked as AggregationUsage=Full should probably be included in every aggregation.
1. No aggregation should have redundant attributes as that will bloat the size of the aggregation. (For instance, it is redundant to include both Calendar Quarter and Calendar Year in the same aggregation.) Resolve this warning by clicking the Eliminate Redundancy button in the Aggregation Editor.
1. No aggregation can include an attribute below granularity.
1. For any dimension with a parent-child attribute which has a DefaultMember or is not aggregatable, the key attribute of that dimension should probably be included in every aggregation.

Any questions or comments on these rules and best practices can be discussed in [this thread](http://bidshelper.codeplex.com/discussions/16498)

You can download a sample report generated against the Project REAL cube: [ValidateAggsSample.pdf](Validate Aggregations_ValidateAggsSample.pdf)