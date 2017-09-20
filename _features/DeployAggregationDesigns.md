---
title: Deploy Aggregation Designs
category: ssas
component: ssasm
---

This command deploys just the aggregation designs in a cube. It does not change which aggregation design is assigned to each partition. You should run a ProcessIndex command from Management Studio on this cube after aggregation designs have been deployed.

This command can be launched from the Partitions tab of the cube designer:
![](Deploy Aggregation Designs_DeployAggDesignsTeaser.png)

_Note:_ This command does not deploy any objects on which an aggregation design might depend. For instance, if you have added a new dimension attribute and have built an aggregation on that attribute, you will not be able to use the Deploy Aggregation Designs feature without error until you manually deploy that dimension change.

_Note:_ This feature is not available when editing a cube in online mode as there is no need to deploy when you are working in online mode.