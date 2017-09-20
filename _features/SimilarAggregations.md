---
title: Similar Aggregations
category: ssas
component: ssasm
---

The Similar Aggregations feature allows you to view a report that lists any aggregations which are very similar to each other. Particularly, it looks for pairs of aggregations in which one aggregation is a further summarization of the other. In this case, if both aggs are about the same sizes, one agg can serve to answer queries at both granularities without much loss of performance. This report can be used to identify potential aggregations to remove.

The Similar Aggregations report can be launched from the Aggregation Editor window from [Aggregation Manager](../AggregationManager):

![](Similar Aggregations_SearchSimilarAggsButton.png)

It can also be launched for the entire cube from the main Aggregation Manager window:

![](Similar Aggregations_SearchSimilarAggsMenu.png)

You can download a sample report: [SearchSimilarAggs.pdf](Similar Aggregations_SearchSimilarAggs.pdf)

Note that this report only shows you which aggregations are contained within other aggregations. If you want to quantify MDX query performance with each agg, without all aggs, and with similar aggs, use the [Test Aggregation Performance](../TestAggregationPerformance) feature.

**Acknowledgements:** Many thanks go out to Leandro Tubia for providing us with this code.