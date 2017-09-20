---
title: Expression List
category: ssis
component: ssis
---

The Expression List provides a window that lists all the expressions defined in a package. When you have an SSIS project open, the Expression List can be shown or hidden by going to the View... Other Windows menu and selecting the "Expression List (*{{site.title}}*)" menu item:

![](Expression List_ExpressionListMenu.png)

![](Expression List_ExpressionsList.png)

Refreshing the list is a manual process, just click Refresh. The window  shows the following information:

| Column | Description |
|---|---|
| **Object Type** | The type of the object on which the expression is defined upon. |
| **Path** | The path to the expression object. Especially useful when you have nested objects or expressions within event handlers. |
| **Property** | The name of the property or object that the expression applies to. |
| **Expression** | The expression itself. Click the button to edit the expression. |

The expression list searches the entire package, including tasks, loops, event handlers, precedence constraints and variables looking for expressions.

The elipsis button located in the far right column of the grid diplay opens an Expression Editor, provided by Konesans ([http://www.konesans.com](http://www.konesans.com)).

![](Expression List_ExpressionEditor.png)

The Expression Editor component is now also available on CodePlex - [SSIS Expression Editor & Tester](http://expressioneditor.codeplex.com/)