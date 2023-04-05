+++
archetype = "chapter"
title = "Area Graphs"
weight = 5
+++

Area graphs are different (more simpler) than the other node graphs in Eldiron:

* They do not use behavior trees
* Graphs go from left to right instead from top to bottom.
* The graph do not offer any scripting capabilities.

Area graphs can be edited in the [region editor](../regions_edit_areas.md) in Eldiron.

Instead of behavior trees, drag and drop one of these nodes into the graph:

* [Action](../nodes/action.md). To create feedback on user based actions. For example when the user looks at the area (which could be a sign or anything else which requires some kind of response).
* [Always](../nodes/always.md). To always perform some constant action. For example a light source.
* [Enter Area](../nodes/enter_area.md). Create some action or response when a character enters an area (for example to open a door).
* [Leave Area](../nodes/leave_area.md). Create some action or response when a character exits an area (for example to close a door).
* [Inside Area](../nodes/inside_area.md). Create some action or response when a character is inside an area (for example apply damage over time when inside a trap).

The state of these nodes are evaluated on every game tick.
