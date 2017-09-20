---
title: Installing from the Visual Studio Gallery
component: common
---

*{{site.title}}* for SQL 2016 is installed in Visual Studio 2015 and this version of the add-in is published in the Visual Studio Gallery. To install it, go to Tools... Extensions and Updates... go to the Online tab and then search for *{{site.title}}*:

![](Installing from the Visual Studio Gallery_BIDSHelperVSGallery.png)

You can also download it from the Visual Studio Gallery in a web browser [here](https://marketplace.visualstudio.com/vsgallery/e8c17a53-f117-426d-9e92-407115777d6e).

**KNOWN ISSUE:** When installing SSDT, install SSAS, SSRS, and SSIS. *{{site.title}}* does not currently support partial installs of SSDT.

**KNOWN ISSUE:** For now, for *{{site.title}}* to be compatible in VS2015 you need to use the SSDT 16.5 for VS2015 found [here](https://docs.microsoft.com/en-us/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi).

To know if you have that installed, your Help... About Microsoft Visual Studio will say:
Microsoft SQL Server Analysis Services Designer 
Version 13.0.1701.8

If you must use SSDT 17.0 in VS2015 then click [furmangg](https://www.codeplex.com/site/users/view/furmangg) and shoot me an email to become a beta tester as we work on support for the recently released version that's compatible with SQL 2017