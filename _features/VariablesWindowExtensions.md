--- 
title: SSIS Variables Window Extensions
layout: feature
category: ssis
component: ssis
---
# SSIS Variables Window Extensions

This feature is designed to extend the Variables window in the SSIS package designer. Currently the extension:
* Highlights the variable icons when expressions or package configurations impact them. (See the [Expression and Configuration Highlighter](../ExpressionandConfigurationHighlighter) feature for more information about colours and highlighting.)
* Adds a button that lets you move or copy a variable to another scope in that package.
* Adds a button that lets you edit the expression on a variable using the custom  [expression editor](http://expressioneditor.codeplex.com/). The edit expression ellipsis button on each grid line will also invoke the custom editor (Pre-Release)
* Adds a button to find all references to the currently selected variable (Pre-Release)
* Adds a button to find all unused variables (Pre-Release)

![](Variables Window Extensions_VariablesWindowButtons.png)

## Move / Copy Variable to New Scope
Select the variables you wish to move or copy then click the button. You get the following popup that allow you to choose the new scope for those variables:

![](Variables Window Extensions_MoveOrCopyVariables.png)

The move or copy is executed. Then the package is revalidated and the Error List window is updated with any validation errors. For instance, if a task or expression was referring to that variable in the old scope, the package will not validate any more, and you will need to identify the problem and make the appropriate edits in the package designer to fix the problem.

You can also edit the expression on a variable using the [SSIS Expression Editor](http://expressioneditor.codeplex.com/), as also used in the [Expression List](../ExpressionList):

![](Variables Window Extensions_VariablesWindowEditExpressionButton.png)

## Find Variable References
Select a variable in the variables window, and then click the _Find Variable References_ button to show the references dialog with all uses of the variable shown in a package explorer style dialog.

![](Variables Window Extensions_FindVariableReferences.png)

The _Find Unused Variables_ feature will display a dialog listing any variables that are not used in the package, You can then select one or more variables and remove them.

![](Variables Window Extensions_FindUnusedVariables.png)

Similar functionality is available for package parameters, see [Parameter Window Extensions](../ParameterWindowExtensions).