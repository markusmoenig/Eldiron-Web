+++
title = "Behavior Trees"
weight = 1
+++

![Graphs and Scripts](./../graphs_scripts.png)

Every node graph in Eldiron (except [area nodes](./../area_graphs/) which are a bit more simple) utilizes behavior trees to break up the overall behavior into smaller, easily understandable chunks (trees).

A behavior tree is just a node with several terminals at the bottom which get executed from left to right. You typically rename the behavior tree to indicate what behavior the tree is executing, for example *Go Raiding*, or *Talk* and *Combat*.

In a programming language behavior trees would be similar to functions.

Every behavior tree node has an *Execute* property which indicates when the tree is executed:

- **Always**. The behavior tree is always executed if the graph is not locked.
- **On Startup**. The behavior tree is only executed once when the graph is created.
- **On Demand**. The behavior tree is executed on demand.

Behavior trees perform the AI for non-player-characters (NPCs) and connect input commands from the *Player* character to the right player action.

All behavior trees in a graph are listed as tabs at the top of the graph. Select the given behavior to edit it.

## Active vs. Passive

There are some behavior trees which have a passive behavior and need to end with an " (P)". For example lets assume you have a healer character named Antony. When your player performs a custom action in a given direction Eldirons node system checks if the character (or item) located in the given direction has a behavior node tree called *"ActionName (P)"*. For example lets say the player looks towards Antony and you want to send a message to the player:

* Create a new behavior tree for Antony (by dragging a [Behavior Tree](../../../reference/nodes/#behavior-tree) node into the graph).
* Rename the node to "Look (P)"
* Attach a [Message](../../../reference/nodes/#message) node to it with a status message like "You see Antony, a famous healer.".

Make sure that the behavior tree is set to execute "On Demand".

One big difference between passive behavior trees and normal ones is that passive behavior trees use the context of the caller instead of their own. You do not want to send the message to Antony but to the player who is looking in his direction. Thats why the convention with the naming is important to mark this difference.

{{% notice style="tip" %}}
The same *look* behavior is also possible with area nodes by utilizing the [Action](../../../reference//nodes/#action) node. For example if you look at a sign and want to send a message to the player. For more information about area nodes see [the edit areas section](../regions_edit_areas.md).
{{% /notice %}}

## Behavior Trees vs System Trees

Creating behavior trees for characters is fine. But if you want to implement general systems like crafting or magic you do not want to implement them again and again for every player character in the game. This is where system trees come into play. Go to the [systems view](../systems.md) and create behavior trees for a given system like you would for characters. Now in your characters you can call these trees with the [Call System](../nodes/call_system.md) node. They execute the same way as would your local trees with the same character context. This way you can create re-usable systems for your game.

{{% notice style="tip" %}}
To create a new behavior tree just drag and drop a *Behavior Tree* node item into the node graph.
{{% /notice %}}
