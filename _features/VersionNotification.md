---
title: Version Notification
component: common
---

*{{site.title}}* is constantly adding new features and fixing recently discovered bugs. We encourage everyone to use the latest version. The Version Notification feature helps you stay current by alerting you when a new *{{site.title}}* version is released. A balloon and icon appear in the system tray. Click the balloon and *{{site.title}}* will open Internet Explorer and take you to the download page for the latest release.

![](Version Notification_VersionNotification.png)

If you do not have time at that moment to install the latest *{{site.title}}*, right click on the *{{site.title}}* icon and choose to have *{{site.title}}* remind you later (in 7 days).

If you are not interested in installing that particular version, but you wish to be notified about future releases, you can dismiss the notification about that particular version.

![](Version Notification_VersionNotificationContextMenu.png)

*{{site.title}}* checks to see that you have the latest version once a week. If you ever want to validate that you have the latest version installed, go to the Tools menu and choose Options then expand the *{{site.title}}* tree, then click Version. When that Version screen opens, it shows you the version of *{{site.title}}* you have installed and also checks to make sure you have the latest installed:

![](Version Notification_VersionOptionsScreen.png)


Starting with *{{site.title}}* 1.6.3, the Version screen also displays some information about your version of SQL Server development tools, your version of Visual Studio, and any problems that occurred trying to start *{{site.title}}*:

![](Version Notification_VisualStudioVersion.png)

For example...

* "SSDTBI 2012 for Visual Studio 2012 was detected" means that you have installed the SQL Server 2012 developer tools (properly named SSDTBI) and that you are currently in Visual Studio 2012.
* "BIDS 2008 R2 for Visual Studio 2008 was detected" means that you have installed the SQL Server 2008 R2 developer tools (named BIDS) and that you are currently in Visual Studio 2008.
* "SSDTBI for Visual Studio 2012 was NOT detected. *{{site.title}}* disabled." means that you do not have the SQL Server developer tools installed for Visual Studio 2012 so *{{site.title}}* is not running.
* "BIDS for Visual Studio 2008 was NOT detected. *{{site.title}}* disabled." means that you do not have the SQL Server developer tools installed for Visual Studio 2008 so *{{site.title}}* is not running.
