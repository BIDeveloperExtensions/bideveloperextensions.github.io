---
title: Design Warnings
category: ssis
component: ssis
---
The SSIS Design Warnings feature provides similiar functionality to the Design Warning feature in Analysis Services 2008. It compares the current package against a list of design guidelines, and adds warnings to the Error List in Visual Studio for any items that need to be investigated. A package can be scanned for design warnings by right-clicking on it in the Solution Explorer and choosing the Design Warnings Scanner option from the pop-up menu.
![](Design Warnings_DesignWarnings.gif)

The warnings will appear in the Error List in Visual Studio.
![](Design Warnings_ErrorList.gif)

The following warnings have either been implemented, or are under consideration:

| Status | Warning Name | Description | Reason |
| ------ | ------------ | ----------- | ------ |
| Build 1.4.2 | Connection Configurations | Validates that the ConnectionString property for all Connection Managers has either a configuration or an expression applied | Using configurations on connection strings makes the packages easier to deploy to different environments |
| Build 1.4.2 (2008 only) | Data Flow Asynchronous Paths | Validates that there are no asynchronous outputs (excluding source components) | Asynchronous outputs are slower than synchronous outputs, due to the fact that the values in the buffer have to be copied to a new memory location. They should be used sparingly. |
| Build 1.4.2 | Data Flow Count | Validates that there is only one data flow per package | Breaking large packages with multiple data flows down into multiple packages with a single data flow makes maintenance of the packages easier, and facilitates distributing the workload across multiple developers. |
| Build 1.4.2 (2008 only) | Data Flow Sort Transformations | Adds a warning if it identifies Sort transformations that can be moved to a database. It will also add a warning if it detects more than 2 Sort transformations in the data flow. | Sort transformations are fully blocking, meaning that they must take all rows in before they can output any rows. This can lead to many performance issues. Ideally, the data should be sorted in a database, rather than using the Sort transformation. |
| Build 1.4.2 | Access Mode | Validates that Source and Lookup components are not using the "Table or View" access mode | The "Table or View" access mode uses an OpenRowset statement to retrieve the data. This performs slower than using an SQL statement, and may bring back unnecessary columns. |
| Build 1.4.2 | Package ProtectionLevel | Validates that the ProtectionLevel property is set to DontSaveSensitive or ServerStorage. | Using ServerStorage for packages stored in SQL Server, or DontSaveSensitive with appropriately secured configurations, makes packages easier to deploy and share with other developers. |