+++
title = "Gaining Experience"
weight = 5
alwaysopen = true
+++

Character progress in Eldiron is done via level trees. A [Level Tree](../../nodes/#level-tree) is a node you can insert into any *Systems* object. It connects to a chain of [Level Node](../../nodes/#level-nodes) nodes, each representing a node which gets executed when a specific experience level is reached.

A level tree is automatically discovered and used in the system *class* object of your character. However you can Point Eldiron to custom level tree node locations using the [Set Level Tree](../../nodes/#set-level-tree) node in a startup tree of your character.

![Level Trees](./level_trees.png)

This simple level tree with only two levels is an example of a level tree. The level tree node enables you to enter the message which is shown to the player every time his character gains experience.

The level nodes represent each level, the *Starts at* parameter displays the total experience needed to gain to this level, the *Message* attribute is the message which is displayed to the user when he gains the level and finally the *Script* parameter is the script which gets executed when the user reaches this level, in the script you can modify the characters sheet as needed.

### Increasing Experience

As discussed [Increasing Experience](../../scripting/server/#increasing-experience) you can add experience to the character using the ```sheet = increase_experience_by(sheet, 10);``` function.