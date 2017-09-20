---
title: Dimension Optimization Report
category: ssas
component: ssasm
---

Right-clicking on the Dimensions folder lets you open a report about dimension optimization settings:

![](Dimension Optimization Report_DimensionOptimizationReport.png)

The report looks like the following:

![](Dimension Optimization Report_DimensionOptimizationReportPreview.gif)

This report lists all dimension attributes and hierarchies on rows. On columns, it lists various properties which can be used to optimize dimensions. The first set of columns are properties on the dimension attributes themselves. The remaining sets of columns are properties on the cube dimension attributes. Download a [sample](Dimension Optimization Report_DimensionOptimization.xls) report for Adventure Works. The report contains the following columns:

* **Dimension Properties**
	* _Estimated Count_ - This property gives you an idea of the cardinality of this dimension attribute. (Consider running [Update Estimated Counts](../UpdateEstimatedCounts) if it is out-of-date.) The Estimated Count will give you an idea of how expensive it will be to order and index this attribute.
	* _Enabled_ - This column reflects the AttributeHierarchyEnabled setting on a dimension attribute. If you don't need to slice by this attribute but need it only as a member property, set AttributeHierarchyEnabled=False.
	* _Optimized State_ - This column reflects the AttributeHierarchyOptimizedState property. If this attribute is used infrequently in queries, set it to NotOptimized to skip building indexing of partitions and aggregations against this attribute.
	* _Visible_ - This column reflects the AttributeHierarchyVisible property.
* **Cube Dimension Attribute Properties**
	* _Aggregation Usage_ - This column reflects the AggregationUsage property, and it is a hint to the Aggregation Design Wizard.
	* _(Effective) Enabled_ - This column reflects the effective setting when the AttributeHierarchyEnabled property (of the dimension attribute) and the AttributeHierarchyEnabled property (of the cube dimension attribute) are combined. Changing the cube dimension attribute's AttributeHierarchyEnabled setting can only disable a cube dimension attribute hierarchy; it cannot re-enable the attribute hierarchy if the AttributeHierarchyEnabled setting on the dimension attribute is False.
	* _(Effective) Optimized State_ - This column reflects the effective setting when the AttributeHierarchyOptimizedState property (of the dimension attribute) and the AttributeHierarchyOptimizedState property (of the cube dimension attribute) are combined. Changing the cube dimension attribute's AttributeHierarchyOptimizedState setting can only disable indexing; it cannot re-enable indexing if the AttributeHierarchyOptimizedState setting on the dimension attribute is NotOptimized. This column will also show FullyOptimized if this attribute is part of a user-defined hierarchy which is Enabled and FullyOptimized (because in such a situation, this attribute will be indexed).
	* _(Effective) Visible_ - This column reflects the effective setting when the AttributeHierarchyVisible property (of the dimension attribute) and the AttributeHierarchyVisible property (of the cube dimension attribute) are combined. Changing the cube dimension attribute's AttributeHierarchyVisible setting can only hide a cube dimension attribute hierarchy; it cannot make the attribute hierarchy visible again if the AttributeHierarchyVisible setting on the dimension attribute is False.

Johan Rastenberger has some good [suggestions](http://blog.riket.com/index.php?id=5) for the recommended settings depending upon how you intend to use a particular dimension attribute.
