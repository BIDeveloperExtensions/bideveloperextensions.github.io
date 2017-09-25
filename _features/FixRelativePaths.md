---
title: Fix Relative Paths
category: ssis
component: ssis
---

This feature is helpful in setting up packages to use relative paths in connection managers and in the path to dtsConfig files. It was mainly coded to workaround this [bug](https://connect.microsoft.com/SQLServer/feedback/ViewFeedback.aspx?FeedbackID=355433) in SQL2008, but it can also be helpful in SQL2005.

For more information about using relative paths in SSIS, see this [blog post](http://www.artisconsulting.com/blogs/greggalloway/2008/7/13/relative-paths-in-ssis).

This feature adds a "Fix All Relative Paths" button to the Package Configurations dialog:

![](Fix Relative Paths_FixRelativePathsPackageConfigurationDialog.png)

Clicking that button will change full paths (i.e. "c:\Directory\test.dtsConfig") to relative paths (i.e. "test.dtsConfig") if the following are true:
* If the working directory for the current Visual Studio process is the same directory as the current package.
* If the package configuration is an XML file and the dtsConfig file is in that same directory.

This feature can also be run on multiple packages simultaneously by using the right-click menu item on the project node in Solution Explorer:

![](Fix Relative Paths_FixRelativePathsMenu.png)

When selected, *{{site.title}}* will scan all open packages. Inside each package, it will scan all XML file package configurations and all connection managers looking for full paths which point to a file in the same directory as the package. The restriction mentioned above about the working directory for Visual Studio still applies.

The results of this command can be seen in the Output Window:

![](Fix Relative Paths_FixRelativePathsOutputWindow.png)