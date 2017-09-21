---
title: Deploy SSIS Packages
category: ssis
component: ssis
---

This feature lets you quickly deploy SSIS packages directly from {{site.ms-designer}} without having to create a deployment manifest and use the Package Installation Wizard.

First, right click on the project node in Solution Explorer and choose Properties.

![](Deploy SSIS Packages_DeployPackagesMenus.png)

*{{site.title}}* adds a custom tab to the screen that pops up. Flip to the "Deploy (*{{site.title}}*)" tab and edit the properties to specify how you want to deploy your solution.

![](Deploy SSIS Packages_DeployPackagesConfigurations.png)

The following types of deployment mechanisms are supported:
* _Simple File Copy_ - Copies packages to any windows directory.
* _SQL Server Destination_ - Copies packages into MSDB in the specified SQL Server instance.
* _SSIS Package Store (File System)_ - Copies packages into the SSIS Package Store on the file system of the specified server. (The files end up in "C:\Program Files\Microsoft SQL Server\90\DTS\Packages" by default.)
* _SSIS Package Store (MSDB)_ - Copies packages into the SSIS Package Store in MSDB on the specified server.

It is recommended that you click the Configuration Manager button in this dialog and create one Visual Studio configuration per deploy destination (i.e. Development, Staging, Production). *{{site.title}}* allows you to save separate deployment destination settings per Visual Studio configuration.

When you click the OK button, your *{{site.title}}* settings for Deploying SSIS Packages are saved into a file in the project directory called <ProjectName>.dtproj.bidsHelper.user.

Next, deploy packages by right clicking on the packages you wish to deploy in Solution Explorer and choosing Deploy. You may right click on a single package, you may Ctrl-click multiple packages then right click on them, or you may right click on the project node to deploy all packages in the project. If you have multiple projects in the solution, all of which are SSIS projects, you can right click on the solution node and deploy all packages from all projects using that menu option.

The Output window displays details about the progress of your deployment:

![](Deploy SSIS Packages_DeployPackagesOutput.png)

If deploying an entire project (via the project node menu or the solution node menu), a file is created in the OutputPath (usually the bin directory) called bidsHelperDeployPackages.bat which contains all the commands which were just used to deploy the packages. This bat file can be used as a starter for automating deployment.

**Limitations:**
* SSIS Package Configurations are not deployed. No dtsConfig files can be deployed using *{{site.title}}*. *{{site.title}}* will **not** alter your packages or modify your package configurations. Package configurations should be manually setup on the destination environment before deploying your packages.
* Only Windows Integrated Security is supported for deploying packages to SQL Server or the SSIS Package Store.
* Packages encrypted with a password are not supported with the Deploy Packages feature unless you set DeploymentType=FilePathDestination (which is just a simple file copy that does not use dtutil and thus does not need to decrypt the package).
* If you have customized your MsDtsSrvr.ini.xml, *{{site.title}}* does not account for this when deploying packages. Please follow and vote for issues [workitem:27127](http://bidshelper.codeplex.com/workitem/27127) and [workitem:22297](http://bidshelper.codeplex.com/workitem/22297) if this impacts you.
* This feature is not available in SSIS2012 when your project is in "[project deployment model](https://www.mattmasson.com/2012/07/can-i-deploy-a-single-ssis-package-from-my-project-to-the-ssis-catalog/)", only when it is in legacy "package deployment model". To deploy your project in project deployment model, use the built-in SSIS2012 deployment feature.