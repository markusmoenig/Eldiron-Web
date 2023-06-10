+++
title = "Behavior Trees"
weight = 1
alwaysopen = true
+++

Behavior trees are one of the main mechanics in Eldiron. They consist of a [Behavior Tree](../../nodes/#behavior-tree) node which has up to 3 nodes connected to its bottom terminals (the nodes get executed from the left to right).

You would rename the behavior tree node based on the action this tree implements, like **Look**. You can implement and invent any action your character should execute via behavior trees. See the [nodes](../../nodes/) section or watch my Youtube videos to learn more about the various behavior nodes availabe to you.

## Active vs Passive

As described above, behavior trees execute commands, for example when you *Look* at something. But what if somebody looks at your character ? In this case the tree on the target is executed with the command name + " (P)" for passive, i.e. "Look (P)". Note that for passive trees, the current character is the character looking at you, as you do not want to send a message to yourself, this is why we call this a passive tree.

## System Trees

Each object in the *Character* view defines a character, which means that each behavior tree of that character is unique to that character, you cannot share behavior trees for characters.

However it would be a lot of work to create each character in the game from scratch. This is where the *Systems* view is for. The *Systems* view contains re-usable objects and trees. You can call a system tree with the [Call System](../../nodes/#call-system) node.

System objects are also used to implement skills and to provide an inheritance mechanism for character races and classes. More about these later.