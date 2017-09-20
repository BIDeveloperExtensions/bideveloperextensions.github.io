---
title: Reset GUIDs
category: ssis
component: ssis
---

This feature resets the IDs for all tasks, connection managers, configurations, event handlers, variables, and the package ID itself. When you copy a package, objects in both packages end up with the same IDs. This Reset GUIDs feature ensures that the IDs in the current package are unique.

Distinct GUIDs help ensure that SSIS logging results are easier to interpret. Also, package debugging in {{site.ms-designer}} works better when task GUIDs are not shared between packages. Plus, this works around a sporadic bug where editing a task with a duplicate ID in one package causes changes to the task in the wrong package. Apparently, duplicate GUIDs can also cause [execution failures](http://datachix.com/2010/01/31/the-case-of-the-mysterious-failing-packages/) and other [designer oddities](http://denglishbi.wordpress.com/2011/03/25/ssis-package-copypaste-new-guid-id-fix/).

![](Reset GUIDs_ResetGuidsMenu.png)

Note: This feature works against the [Smart Diff](../SmartDiff) feature since the new GUIDs cause sorting in Smart Diff to change. So do not expect Smart Diff results to be intelligible immediately after running Reset GUIDs.