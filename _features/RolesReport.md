---
title: Roles Report
category: ssas
component: 
    - ssasm
    - ssast
compatibilitylevel:  
    - 1103
    - 1200
    - 1400
---

The main purposes of this Roles Report are the following goals:

1. To recursively list the members of the role and the members of groups so that you can easily determine which members actually have access via each role.
1. To identify members of roles which will not have the desired effect. Specifically if a role references an Active Directory group which is a distribution group instead of a security group, members of that group will not gain the access granted with the role. This report highlights this situation.
1. To identify members of roles which are invalid and which are causing the "no mapping between account names and security IDs was done" error during deployment.
1. To summarize all the security permissions granted via the roles instead of having to click into dozens of screens to find this information.
1. To serve as documentation which can be printed or archived or sent to non-developers.

Right-clicking on the Roles folder in an SSAS Multidimensional project lets you open a report summarizing everything about the setup of those roles:

![](Roles Report_RolesReportMenu.png)

The first pages of the report list the members of each role:

![](Roles Report_RolesReportMembersScreenshot.png)

The other pages detail the permissions granted in each role such as the following summary of dimension data security:

![](Roles Report_RolesReportDimSecurityScreenshot.png)

For a more complete example, download a [sample](Roles Report_RolesReport.pdf) report.

Note: This report can take several minutes to run. Be patient.

Note: Many thanks to Edward Melomed for letting **{{site.title}}** borrow some code from his [ASValidateUsers](http://www.codeplex.com/SQLSrvAnalysisSrvcs/Release/ProjectReleases.aspx?ReleaseId=13572) tool.


#### Tabular Models
Starting with release 1.6.5, the Roles Report is available for Analysis Services Tabular Models. In Solution Explorer, right click on the .bim file to launch this report.

![](Roles Report_RolesReportMenuTabular.png)

It displays a simplified version of the report which is appropriate for the role security definition of Tabular models.