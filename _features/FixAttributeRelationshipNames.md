---
title: Fix Attribute Relationship Names
category: ssas
component: ssasm
---

In Analysis Services Multidimensional, attribute relationships typically bear the name of the related attribute. However, it is possible to rename the attribute relationship or rename the attribute, both of which cause those two names to be out of sync. When this happens, SSDT warns you with a blue squiggly. Notice the attribute is named "Description" and the attribute relationship is named "Desc".

![](AttributeRelationshipNameWarning.png)

Fixing these mismatches can be tedious. Starting with release 2.2.1, BI Developer Extensions has a Fix Attribute Relationship Names feature. Right-click on the dimension in Solution Explorer to launch this feature:

![](FixAttributeRelationshipNames.png)

