---
title: Many-to-Many Matrix Compression
category: ssas
component: ssasm
---

The whitepaper entitled [Analysis Services Many-to-Many Dimensions: Query Performance Optimization Techniques](http://www.microsoft.com/downloads/details.aspx?FamilyID=3494E712-C90B-4A4E-AD45-01009C15C665&displaylang=en) outlines several techniques to optimize performance of m2m dimensions. One technique is the matrix relationship optimization technique. Analyzing the data in a m2m relationship to determine whether it can be compressed significantly requires building a complex SQL query. This *{{site.title}}* feature automates this process and returns a report showing how much each m2m relationship can be compressed.

In the Dimension Usage tab of the cube designer, click the button in the toolbar:
![](Many-to-Many Matrix Compression_M2MMatrixCompressionButton.png)

Then the following window pops up. *{{site.title}}* begins running one SQL query at a time in the background.

![](Many-to-Many Matrix Compression_M2MMatrixCompression.png)

This window has the following columns:
* **Checkbox:** Unchecking a checkbox will cancel the SQL query for that m2m relationship.
* **Status:** Shows the status of the SQL query that checks the compression stats of that m2m relationship.
* **Data Measure Group:** The name of the data measure group
* **Intermediate Measure Group:** The name of the intermediate measure group in the m2m relationship. This is the bridge fact table.
* **Original:** The original, uncompressed rowcount of the intermediate measure group.
* **Compressed:** The rowcount of the intermediate measure group after you perform the matrix relationship optimization technique.
* **Reduction %:** (Original-Compressed)/Original
* **Dimension:** The size of the new compressed intermediate dimension, also known as a signature dimension.

_Note: The SQL query is based upon the DSV table tied to the measures in the intermediate measure group. Any partition SQL queries are ignored._

_Note: If an error occurs, then the row is highlighted red. Mousing over that row shows the error message in the tooltip._

_Note: For additional information on building an incremental SSIS package to implement the matrix relationship optimization technique, see this [blog post](http://www.artisconsulting.com/blogs/greggalloway/Lists/Posts/Post.aspx?ID=13)._

_Note: The code for this **{{site.title}}** feature was written independent of the [CompressManyToMany](http://sqlsrvanalysissrvcs.codeplex.com/releases) by Eugene A. Asahara (which he described further [here](http://www.softcodedlogic.com/CompressManyToManyRelationships.htm). This tool could be complementary to **{{site.title}}** tool for m2m relationship compression._