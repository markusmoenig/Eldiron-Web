+++
title = "Mechanics"
weight = 2
alwaysopen = false
draft = true
+++

All game mechanics in Eldiron are either handled via behavior trees or [scripts](../scripting/).

Behavior trees are node graphs which define behavior for a certain activity, like a **Look** or **Attack** functionality for a character.

For player character, the tree to execute is send via an action command from the client. For NPC characters every behavior tree node marked with execute **Always** are executed on every game tick.

![Behavior Trees](behavior_trees.png)