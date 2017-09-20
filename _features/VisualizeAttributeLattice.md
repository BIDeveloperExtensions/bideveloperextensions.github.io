---
title: Visualize Attribute Lattice
component: ssasm
---

This feature allows you to visually see the attribute relationships you have defined for a dimension in an Analysis Services solution.

![](Visualize Attribute Lattice_VisualizeAttributeLatticeTeaser.jpg)

Good attribute relationships are the key to effective aggregations in Analysis Services. By default, all attributes relate directly to the key attribute of the dimension. Such attribute relationships look like this:

![](Visualize Attribute Lattice_AllRelateToKey.jpg)

If possible, indirect relationships are usually preferred:

![](Visualize Attribute Lattice_IndirectRelationships.jpg)

_Limitation:_ If your dimension has a redundant attribute relationship (which will be denoted with a warning at the bottom of the dimension designer), the attribute lattice will probably not render correctly. Please get rid of the redundant attribute relationship.