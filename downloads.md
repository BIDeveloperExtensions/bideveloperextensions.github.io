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

Ensure you have the latest version of [SSDT installed](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017) for Visual Studio 2017. Reference the table below for the targeted SSAS/SSRS/SSIS extension versions. Then in Visual Studio 2017 go to Tools... Extensions and Updates... Updates tab... then ensure you install any updates to Microsoft Analysis Services Projects, Microsoft Reporting Services Projects, or Microsoft Integration Services Projects.

If in Tools... Options... BIDS Helper... Version the SSDTBI Build version isn't at or greater than the SSDTBI Build listed in the table below, you may need to uninstall all SSAS, SSRS, and SSIS extensions then reinstall them. This procedure should update the underlying shared modules.


**Visual Studio 2019**

*{{site.title}}* for Visual Studio 2019 is published in the Visual Studio Marketplace. To install it, go to Extensions... Manage Extensions... go to the Online tab and then search for *{{site.title}}*:

![](/features/InstallingfromtheVisualStudioGallery/Installing from the Visual Studio Gallery_BIDSHelperVSGallery2019.png)

You can also download it from the Visual Studio Marketplace in a web browser [here](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2019).

Ensure you have the latest version of SSDT installed. In Visual Studio 2019 go to Extensions... Manage Extensions... Online tab... then search for BI Developer Extensions. Reference the table below for the targeted SSAS/SSRS/SSIS extension versions.

If in Tools... Options... BIDS Helper... Version the SSDTBI Build version isn't at or greater than the SSDTBI Build listed in the table below, you may need to uninstall all SSAS, SSRS, and SSIS extensions then reinstall them. This procedure should update the underlying shared modules.

**Older Versions**

For SQL 2005 (Visual Studio 2005), SQL 2008 (Visual Studio 2008), SQL 2008 R2 (Visual Studio 2008), download [release 1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v1.7.0).

For SQL 2012 (Visual Studio 2010 and Visual Studio 2012) and SQL 2014 (Visual Studio 2013), though [release 1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v1.7.0) works, we recommend moving development to Visual Studio 2017 which is backwards compatible with SQL 2012 and SQL 2014. For Visual Studio 2017, install {{site.title}} from the Visual Studio gallery using the instructions above.

To install *{{site.title}}* in Visual Studio 2005-2013, download the installer mentioned above. For silent installs you can run the setup .exe file with a /S command line option.

If for some reason you cannot use the installer the latest release includes an [xcopy deploy](/features/xcopydeploy) option.


**Versions Summary**

The following versions of SSDT and BI Developer Extensions are compatible with each other. The bolded lines (Visual Studio 2017 and 2019) are still being maintained.

| Visual Studio Version | SQL Versions | SSDT Installer Version | SSDTBI Build | SSAS Extension Versions  | SSIS Extension Versions  | SSRS Extension Versions  | BI Developer Extensions Version |
|---|---|---|---|---|---|---|
| **2019**  | **2012-2022** | **N/A** | **16.0.19836.0** | **[2.9.18](https://probitools.gallerycdn.vsassets.io/extensions/probitools/microsoftanalysisservicesmodelingprojects/2.9.18/1626109082514/Microsoft.DataTools.AnalysisServices.vsix)**  | **[4.4](https://ssis.gallerycdn.vsassets.io/extensions/ssis/sqlserverintegrationservicesprojects/4.4.2/1674011659205/Microsoft.DataTools.IntegrationServices.exe)** | **[2.6.11](https://probitools.gallerycdn.vsassets.io/extensions/probitools/microsoftreportprojectsforvisualstudio/2.6.11/1632213678395/Microsoft.DataTools.ReportingServices.vsix)** | **[2.4.1](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2019)** |
| 2019  | 2012-2019 | N/A | 15.0.19126.0 | [2.9.12](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)  | 3.9-[3.16](https://ssis.gallerycdn.vsassets.io/extensions/ssis/sqlserverintegrationservicesprojects/3.16/1645603822968/Microsoft.DataTools.IntegrationServices.exe) | [2.6.7](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio) | [2.4.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v2.4.0/BI.Developer.Extensions.2.4.0.for.VS2019.vsix) |
| 2019  | 2012-2019 | N/A | | [2.9.12](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)  | [3.8](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects) | [2.6.7](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio) | [2.3.9](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v2.3.9/BI.Developer.Extensions.2.3.9.for.VS2019.vsix) |
| 2019  | 2012-2019 | N/A | | [2.9.10](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)  | [3.7](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects) | [2.6.7](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio) | [2.3.8](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v2.3.8/BI.Developer.Extensions.2.3.8.for.VS2019.vsix) |
| 2019  | 2012-2019 | N/A | | [2.9.8](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)  | [3.5](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects) | [2.6.5](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio) | [2.3.7](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.7) |
| 2019  | 2012-2019 | N/A | | [2.9.6](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)  | [3.5](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects) | [2.6.3](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio) | [2.3.5](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.5) |
| 2019  | 2012-2019 | N/A | | 2.8.15 - 2.8.17 | [3.1](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects) | [2.5.9](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio) | [2.3.4](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.4) |
| 2019  | 2012-2019 | N/A | | [2.8.14](http://download.microsoft.com/download/D/3/5/D35E9147-77C9-444E-8D89-D95889B1FC2A/Microsoft.DataTools.AnalysisServices.vsix)  | 3.0 | [2.5.7](http://download.microsoft.com/download/2/7/A/27A18FE1-C5CC-46D3-9AC2-B3BBAED5E6C5/Microsoft.DataTools.ReportingServices.vsix)  | [2.3.3](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.3) |
| **2017**  | **2012-2019** | **[15.9.6](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer)** | **15.0.1659.0** | **[2.9.12](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)**  | **2.7**  | **[2.6.7](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)**  | **[2.4.0](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDeveloperExtensionsVS2017)** |
| 2017  | 2012-2019 | [15.9.5](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer) | | [2.9.12](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)  | 2.4  | [2.6.7](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)  | [2.3.9](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v2.3.9/BI.Developer.Extensions.2.3.9.for.VS2017.vsix) |
| 2017  | 2012-2019 | [15.9.5](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer) | | [2.9.10](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)<br/>(or higher)  | 2.4  | [2.6.7](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)  | [2.3.8](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v2.3.8/BI.Developer.Extensions.2.3.8.for.VS2017.vsix) |
| 2017  | 2012-2019 | [15.9.4](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer) | | [2.9.8](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)  | 2.4  | [2.6.5](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)  | [2.3.7](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.7) |
| 2017  | 2012-2019 | [15.9.3](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer) | | [2.9.6](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)  | 2.4  | [2.6.3](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)  | [2.3.5](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.5) |
| 2017  | 2012-2019 | [15.9.2](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer) | | 2.8.15 - 2.8.17  | 2.1 - 2.4  | [2.5.9](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)  | [2.3.4](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.4) |
| 2017  | 2012-2019 | 15.9.0 - 15.9.1 | | 2.8.11 - [2.8.14](http://download.microsoft.com/download/D/3/5/D35E9147-77C9-444E-8D89-D95889B1FC2A/Microsoft.DataTools.AnalysisServices.vsix) | 2.1 - 2.3  | 2.5.6 - [2.5.7](http://download.microsoft.com/download/2/7/A/27A18FE1-C5CC-46D3-9AC2-B3BBAED5E6C5/Microsoft.DataTools.ReportingServices.vsix)  | [2.3.3](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.3.3) |
| 2017  | 2012-2019 | [15.8.2](https://docs.microsoft.com/en-us/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi)<br/>(or older)  | | 2.0  | 2.1  | 2.0  | [2.2.1](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/tag/v2.2.1) |
| 2015  | 2012-2017 | [17.4](https://docs.microsoft.com/en-us/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi?view=sql-server-2017)  | |  |   |   | [2.1.1](https://marketplace.visualstudio.com/items?itemName=BIDSHelper.BIDSHelperforVisualStudio2015)  |
| 2013  | 2014 | [12.0.2430](https://www.microsoft.com/en-us/download/details.aspx?id=42313) |  |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2014Setup.1.7.0.0.exe) |
| 2012  | 2012 | [11.0.5583](https://www.microsoft.com/en-us/download/details.aspx?id=36843) |  |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2012Setup.1.7.0.0.1.exe) |
| 2010  | 2012 | |  |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2012Setup.1.7.0.0.1.exe) |
| 2008  | 2008-2008R2  | | |  |  |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2008Setup.1.7.0.0.exe) |
| 2005  | 2005 | | |  | |  |  [1.7.0](https://github.com/BIDeveloperExtensions/bideveloperextensions/releases/download/v1.7.0/BIDSHelper2005Setup.1.7.0.0.exe) |

