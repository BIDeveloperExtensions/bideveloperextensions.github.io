---
title: Duplicate Role
category: ssas
component: ssasm
---

**Note: this feature is not part of the current stable release, it will be included in the next release.**

This feature allows you to copy a role with all of the associated settings and permissions. This is implemented as a new menu item on the right click menu for a role.

![](Duplicate Role_image_2.png)

If you simply copy and paste a role using the standard functionality all you will end up with is a copy of the role object which basically only contains the role membership. The *{{site.title}}* Duplicate Role feature however will copy _all_ of the permissions and setting for a role including the following:

 - Database Permissions 
 - Cube Permissions
 - Cube Dimension Permissions 
 - Dimension Permissions

Because of this you will noticed that you may need to save (or checkin if you are using source control) some of your cube(s) and dimension(s) after using this feature. However it can save you a lot of time if you want to create a number of similar roles.
