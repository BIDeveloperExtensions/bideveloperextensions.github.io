---
title: Deploy Perspectives
category: ssas
component: ssasm
---

This command deploys just the perspectives in a cube. It also deletes any perspectives on the server which have been removed from source code.

This command can be launched from the Perspectives tab of the cube designer:
![](Deploy Perspectives_DeployPerspectives.png)

_Note:_ This command does not deploy any objects on which an aggregation design might depend. For instance, if you have added a new dimension attribute you are responsible for deploying the dimension first..

_Note:_ This feature is not available when editing a cube in online mode as there is no need to deploy when you are working in online mode.