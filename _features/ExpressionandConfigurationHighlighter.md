---
title: Expression and Configuration Highlighter
component: ssis
---

During development of SSIS packages, it can be easy to overlook that tasks or connection managers are controlled by expressions or package configurations. The purpose of this *{{site.title}}* feature is to give a visual indicator so that the influence of expressions and package configurations can be seen at a glance.

When an expression or package configuration is in effect in a control flow task, data flow task, event handler task, or connection manager, the icon is altered. An expression is indicated with a magenta triangle, a package configuration is indicated with an aqua triangle, and if both an expression and a package configuration are in effect on the same object, a multi-color triangle is used as the indicator:

![](Expression and Configuration Highlighter_ExpressionHighlighterTeaser2.png)

![](Expression and Configuration Highlighter_ExpressionHighlighterTeaser3.png)

All types of package configurations are supported. However, SQL Server package configurations are ignored when the Work Offline setting is checked.

As part of the [Variables Window Extensions](../VariablesWindowExtensions) feature, package variables also show an altered icon when controlled by an expression or a package configuration.

_Performance Warning:_ On very large packages, the expression and configuration highlighting can cause noticeable pauses in the package designer UI. The 1.3 release includes a major revamp of this feature that significantly improves performance. If you find the performance sluggish, consider disabling this feature with the Enabled Features dialog which can be found by choosing Tools... Options... then by choosing *{{site.title}}* on the left. The [Expression List](../ExpressionList) feature can be used as an alternative, as you can control when the expressions are refreshed.

_Note: Starting in release 1.4.2.2, you can edit the colors of the triangles in the [Preferences](../Preferences) screen._

In SSIS 2012, limited expression highlighting is built-in to Integration Services. *{{site.title}}* highlighting has been modified to work properly:

![](Expression and Configuration Highlighter_SSIS2012Highlighting.jpg)