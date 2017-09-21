---
title: Delete Unused Indexes
category: ssas
component: ssasm
---

#### Purpose

Analysis Services Multidimensional models index fact partition data by every dimension attribute by default. When queries slice by a dimension member, these indexes allow the server to scan only the fact partition segments which contain data for that dimension member. Indexes are helpful to query performance (on one large cube, queries performed 40% slower without any indexes).

These indexes are rebuilt during cube processing during the ProcessIndexes phase. For example, ProcessFull on a partition will build these indexes. Also, when you ProcessUpdate a dimension, indexes and flexible aggregations for all partitions are dropped when dimension rollups change, necessitating they be rebuilt with a subsequent ProcessIndexes command. On large cubes, significant time can be spent on building indexes during processing. Also, on committing cube processing transactions on large cubes, hundreds of thousands of index files can slow down the commit as [Andrew Calvett](http://blog.calvett.co.uk/2013/02/21/the-anatomy-of-a-process-update-part-2/) describes.

Specific indexes can be disabled by setting AttributeHierarchyOptimizedState to NotOptimized. In cubes with hundreds of dimension attributes, deciding which indexes are needed and disabling the unused indexes is a very tedious task. This *{{site.title}}* Delete Unused Indexes feature exists to automate this task.

These indexes are the *.map files and often can consume more space than the leaf level partition data (the .fact.data file). For example, in the following screenshot, notice the partition data is 883KB and there are several large indexes. One attribute in the Internet Sales Order Details dimension generates a 201KB index and another from the same dimension generates a 107KB index. An attribute in the Customer dimension generates a 95KB index, etc.

![](Delete Unused Indexes_DeleteUnusedIndexesExplorerBefore.png)

After analyzing the complete workload of queries, the *{{site.title}}* Delete Unused Indexes feature was able to disable indexes on many dimension attributes. None of the largest indexes were being used, and deleting them saves disk space and processing time. You can see in the following screenshot, the number of files in this partition went from 247 to 29:

![](Delete Unused Indexes_DeleteUnusedIndexesExplorerAfter.png)


#### How to Use

In Solution Explorer, right click on the cube and choose Delete Unused Indexes:

![](Delete Unused Indexes_DeleteUnusedIndexesMenu.png)

This feature needs Profiler data. *{{site.title}}* can create a new trace against the server you have set in the project deployment properties. You can also point *{{site.title}}* at a SQL Server table containing a previously logged set of Profiler trace events. Regardless of which option you choose, make sure *{{site.title}}* sees the complete workload of queries against the cube since this feature will disable any indexes not being used during the queries logged.

If you point *{{site.title}}* at a SQL table, make sure the table contains the following events:

* Query Begin
* Query End
* Query Subcube Verbose

And capture the following columns:

* EventClass
* DatabaseName
* ObjectPath
* TextData
* SessionID
* CurrentTime

Note: The SQL table can be a view. In scenarios where there are a few queries users or queries you wish to exclude from consideration, you can create a view to filter the data before presenting it to *{{site.title}}*.

Once it has finished collecting and analyzing trace events, it will provide the following summary of dimension attributes:

![](Delete Unused Indexes_DeleteUnusedIndexes.png)

Make sure that the Subcubes counter in the top right is > 0 reflecting it has captured some Query Subcube Verbose events. 

For any dimension attributes that have a checkmark next to them, *{{site.title}}* will disable index building when you click OK. For dimension attribute with the checkbox unchecked, *{{site.title}}* will ensure that indexing is enabled.

The **green** highlighted attributes are currently indexed but the index was not used during the profiler trace *{{site.title}}* analyzed. *{{site.title}}* will mark these attributes with a checkmark.

The **red** highlighted attributes are currently not indexed but the queries observed during the profiler trace would have used the index if it had been built. *{{site.title}}* will uncheck these so that it will re-enable indexing when you click OK.

The **gray** text attributes have indexing currently disabled.

Once you click OK and once you deploy your changes to the server, you will need to reprocess your cube for index files to be deleted. The easy way is to simply ProcessFull the cube. The more complex but efficient (since it doesn't need to reread the data from the relational database) way is to run ProcessClearIndexes and ProcessIndexes in a transaction using the following [example](Delete Unused Indexes_DeleteUnusedIndexes ProcessIndexes.xmla). (ProcessIndexes alone will not drop indexes that have been disabled.)

Then retest your query workload for performance to ensure no queries slow down after the recommended indexes are disabled. See the Testing section below for information on properly testing.

Clicking the Export button will put a tab delimited table of data in your clipboard. This table represents the recommendations *{{site.title}}* made, not any checkboxes you have subsequently checked or unchecked. You may paste into Excel and sort and format further. 

![](Delete Unused Indexes_DeleteUnusedIndexesExport.png)

The export contains the following columns.

* **Cube Dimension Name**
* **Attribute Name**
* **Number of Slices on This Attribute** - the number of Query Subcube Verbose events which sliced by this attribute in the profiler trace data analyzed.
* **Attribute Cardinality** - The number of members in this attribute hierarchy. The more members, the more expensive the index is to build, typically. However, indexes on large attributes can be helpful to query performance if queries filter by that attribute.
* **Related Partition Count** - The number of partitions in the measure groups related to this dimension attribute. An index is built per related partition, so the higher this number, the more expensive it is to index it.
* **Currently Effective Optimized State** - currently in the source code, is this attribute building indexes or not? This column takes into account the dimension attribute, the hierarchies it is in, and the cube dimension settings. It shows FullyOptimized if it is currently building indexes.
* **Recommendation** - if the background color is green in the grid, this shows "Disable" and if the background color is red this shows "Enable". See above for the meaning of green and red.



#### Testing

The ClearCache XMLA statement will clear most SSAS caches. Unfortunately, it [does not evict fact partition index files from the FileStores cache](https://connect.microsoft.com/SQLServer/feedback/details/809200/have-clearcache-also-clear-the-filestores-cache). 

The only reliable way to evict index files from the cache is to restart the SSAS instance. To reliably test query performance before and after disabling indexes, we suggest you restart SSAS, clear the [Windows system file cache](http://www.artisconsulting.com/blogs/greggalloway/2010/12/29/analysis-services-and-the-case-of-the-standby-cache), then run your query workload. Here is the complete, step-by-step testing outline:


1. Capture the Query Subcube Verbose and queries run against your cube and save the Profiler data to a SQL table as described above.
1. Restart SSAS, clear the system file cache, then run your query workload and time the performance.
1. Run the *{{site.title}}* Delete Unused Indexes feature.
1. Deploy the cube to the server.
1. Run ProcessClearIndexes and ProcessIndexes in a transaction using the following [example](Delete Unused Indexes_DeleteUnusedIndexes ProcessIndexes.xmla)
1. Restart SSAS, clear the system file cache, then run your query workload and time the performance, looking for whether queries perform the same even with some indexes disabled.


#### How it Works

The Query Subcube Verbose trace event is the key to detecting which indexes Analysis Services uses during queries. The following is an example:

```
Dimension 1 [Source Currency](Source-Currency)(Source-Currency) (0 0)  [Source Currency Code](Source-Currency-Code):0  [Source Currency](Source-Currency)(Source-Currency):0
Dimension 2 [Destination Currency](Destination-Currency)(Destination-Currency) (13 0 0)  [Destination Currency](Destination-Currency)(Destination-Currency):[US Dollar](US-Dollar)  [Destination Currency Code](Destination-Currency-Code):0  [?](_):0
Dimension 3 [Date](Date)(Date) (0 39)  [Fiscal Year](Fiscal-Year):0  [Date](Date)(Date):[October 20, 2007](October-20,-2007)
Dimension 4 [Geography](Geography) (0 + * 0 0)  [City](City):0  [State-Province](State-Province):+  [Country](Country):*  [Postal Code](Postal-Code):0  [Geography Key](Geography-Key):0
```

Between the parentheses, the following values can appear:

| Symbol | Description | Index Used? |
| ------ | ----------- | ----------- |
| * | all of the members are requested | No |
| + | some but not all of the members are requested | Yes |
| 0 | this subcube doesn't slice by this attribute | No |
| 1 | this subcube requests the all member | No |
| number > 1 | this subcube requests this specific member | Yes |
| - | below granularity slice | Yes |

So in the example above, the following indexes are used: 

\[Destination Currency](Destination-Currency)(Destination-Currency).\[Destination Currency](Destination-Currency)(Destination-Currency), \[Date](Date)(Date).\[Date](Date)(Date), and \[Geography](Geography).\[State-Province](State-Province)


To disable an index, *{{site.title}}* will set the AttributeHierarchyOptimizedState to NotOptimized on the cube dimension attribute. If that dimension attribute is in a hierarchy, the OptimizedState property of that cube hierarchy will be set to NotOptimized (since indexes are always built for levels in hierarchies unless OptimizedState=NotOptimized on the hierarchy).

To enable an index, *{{site.title}}* will ensure AttributeHierarchyOptimizedState is FullyOptimized on the dimension attribute (seen under the dimension designer, not the cube designer, because if a dimension attribute is NotOptimized, it cannot be set to FullyOptimized using the cube attribute's properties). Then *{{site.title}}* ensures the cube attribute's AttributeHierarchyOptimizedState is set to FullyOptimized.

To view the cube attribute and cube hierarchy properties, look in the bottom left corner of the cube designer in BIDS or SSDTBI. We also recommend you run the [Dimension Optimization Report](../DimensionOptimizationReport) and read that documentation page to further explain the rules around when indexes are built.

The Query Begin event is also parsed and if it is a drillthrough query, the Query Subcube Verbose events are skipped for that query. Drillthrough queries set the slice on most attributes and would cause *{{site.title}}* to rarely recommend disabling any indexes. Test performance of drillthrough queries before and after disabling indexes.


#### Limitations

* It is important that the profiler trace is from a time range during which changes to the dimensionality of the cube didn't change. For example, don't attempt to use Profiler logs from January 1 to January 8 if on January 3 you added one dimension attribute and deleted a few others. This will throw off the Query Subcube Verbose parsing logic and will recommend the wrong indexes be deleted.
* Test query performance before and after to ensure disabling the recommended indexes doesn't reduce query performance.
* There are some corner cases such as [arbitrary shapes](http://blog.kejser.org/2006/11/16/arbitrary-shapes-in-as-2005/) which will not be reflected in Query Subcube Verbose in a way that will enable *{{site.title}}* to detect certain indexes are used. 



