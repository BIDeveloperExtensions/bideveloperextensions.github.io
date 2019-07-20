---
title: Downloads
layout: page
redirect_from: "/features/InstallingfromtheVisualStudioGallery/"
---

**Visual Studio 2015**

*{{site.title}}* for Visual Studio 2015 is published in the Visual Studio Marketplace. To install it, go to Tools... Extensions and Updates... go to the Online tab and then search for *{{site.title}}*:

![](/features/InstallingfromtheVisualStudioGallery/Installing from the Visual Studio Gallery_BIDSHelperVSGallery.png)

You can also download it from the Visual Studio Marketplace in a web browser [here](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDSHelperforVisualStudio2015).


**Visual Studio 2017**

*{{site.title}}* for Visual Studio 2017 is published in the Visual Studio Marketplace. To install it, go to Tools... Extensions and Updates... go to the Online tab and then search for *{{site.title}}*:

![](/features/InstallingfromtheVisualStudioGallery/Installing from the Visual Studio Gallery_BIDSHelperVSGallery2017.png)

You can also download it from the Visual Studio Marketplace in a web browser [here](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2017).

Ensure you have the latest version of [SSDT installed](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017) (version 15.9.2 or higher) for Visual Studio 2017. Then in Visual Studio 2017 go to Tools... Extensions and Updates... Updates tab... then ensure you install any updates to Microsoft Analysis Services Projects, Microsoft Reporting Services Projects, or Microsoft Integration Services Projects. This release is designed to work with version 2.8.15 SSAS extension or higher, version 2.5.9 SSRS extension or higher, and 2.1 SSIS extension or higher.



**Visual Studio 2019**

*{{site.title}}* for Visual Studio 2019 is published in the Visual Studio Marketplace. To install it, go to Extensions... Manage Extensions... go to the Online tab and then search for *{{site.title}}*:

![](/features/InstallingfromtheVisualStudioGallery/Installing from the Visual Studio Gallery_BIDSHelperVSGallery2019.png)

You can also download it from the Visual Studio Marketplace in a web browser [here](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2019).

Ensure you have the latest version of SSDT installed. In Visual Studio 2019 go to Extensions... Manage Extensions... Online tab... then search for BI Developer Extensions. This release is designed to work with version 2.8.15 SSAS extension or higher, version 2.5.9 SSRS extension or higher, and 3.0 SSIS extension or higher.

**Older Versions**

For SQL 2005 (Visual Studio 2005), SQL 2008 (Visual Studio 2008), SQL 2008 R2 (Visual Studio 2008), download [release 1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v1.7.0).

For SQL 2012 (Visual Studio 2010 and Visual Studio 2012) and SQL 2014 (Visual Studio 2013), though [release 1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v1.7.0) works, we recommend moving development to Visual Studio 2017 which is backwards compatible with SQL 2012 and SQL 2014. For Visual Studio 2017, install {{site.title}} from the Visual Studio gallery using the instructions above.

To install *{{site.title}}* in Visual Studio 2005-2013, download the installer mentioned above. For silent installs you can run the setup .exe file with a /S command line option.

If for some reason you cannot use the installer the latest release includes an [xcopy deploy](/features/xcopydeploy) option.


**Versions Summary**

The following versions of SSDT and BI Developer Extensions are compatible with each other. The bolded lines (Visual Studio 2017 and 2019) are still being maintained.

| Visual Studio Version | SQL Versions | SSDT Installer Version | SSAS Extension Versions  | SSIS Extension Versions  | SSRS Extension Versions  | BI Developer Extensions Version |
|---|---|---|---|---|---|
| **2019**  | **2012-2019** | **N/A** | **2.8.15 - [2.8.17](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)**  | **[3.1](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects)** | **[2.5.9](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)** | **[2.3.4](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2019)** |
| 2019  | 2012-2019 | N/A | [2.8.14](http://download.microsoft.com/download/D/3/5/D35E9147-77C9-444E-8D89-D95889B1FC2A/Microsoft.DataTools.AnalysisServices.vsix)  | 3.0 | [2.5.7](http://download.microsoft.com/download/2/7/A/27A18FE1-C5CC-46D3-9AC2-B3BBAED5E6C5/Microsoft.DataTools.ReportingServices.vsix)  | [2.3.3](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.3) |
| **2017**  | **2012-2019** | **[15.9.2](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer)** | **2.8.15 - [2.8.17](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)**  | **2.1 - 2.4**  | **[2.5.9](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)**  | **[2.3.4](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2017)** |
| 2017  | 2012-2019 | 15.9.0 - 15.9.1 | 2.8.11 - [2.8.14](http://download.microsoft.com/download/D/3/5/D35E9147-77C9-444E-8D89-D95889B1FC2A/Microsoft.DataTools.AnalysisServices.vsix) | 2.1 - 2.3  | 2.5.6 - [2.5.7](http://download.microsoft.com/download/2/7/A/27A18FE1-C5CC-46D3-9AC2-B3BBAED5E6C5/Microsoft.DataTools.ReportingServices.vsix)  | [2.3.3](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.3) |
| 2017  | 2012-2019 |[15.8.2](https://docs.microsoft.com/en-us/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi)<br/>(or older)  | 2.0  | 2.1  | 2.0  | [2.2.1](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.2.1) |
| 2015  | 2012-2017 | [17.4](https://docs.microsoft.com/en-us/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi?view=sql-server-2017)  |   |   |   | [2.1.1](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDSHelperforVisualStudio2015)  |
| 2013  | 2014 | [12.0.2430](https://www.microsoft.com/en-us/download/details.aspx?id=42313) |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2014Setup.1.7.0.0.exe) |
| 2012  | 2012 | [11.0.5583](https://www.microsoft.com/en-us/download/details.aspx?id=36843) |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2012Setup.1.7.0.0.1.exe) |
| 2010  | 2012 | |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2012Setup.1.7.0.0.1.exe) |
| 2008  | 2008-2008R2 | |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2008Setup.1.7.0.0.exe) |
| 2005  | 2005 | |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2005Setup.1.7.0.0.exe) |


