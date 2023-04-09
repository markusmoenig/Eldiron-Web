+++
title = "Nodes"
weight = 1
+++

### Control Flow Nodes

* [Behavior Tree](#behavior-tree)
* [Expression](#expression)
* [Has State ?](#has-state)
* [Has Target ?](#has-target)
* [Linear](#linear)
* [Schedule](#schedule)
* [Sequence](#sequence)

### Action Nodes

* [Audio](#audio)
* [Call Behavior](#call-behavior)
* [Call System](#call-system)
* [Close In](#close-in)
* [Deal Damage](#deal-damage)
* [Drop Inventory](#drop-inventory)
* [Effect](#effect)
* [Heal](#heal)
* [Light](#light)
* [Lock Tree](#lock-tree)
* [Lookout](#lookout)
* [Message](#message)
* [Multi Choice](#multi-choice)
* [Pathfinder](#pathfinder)
* [Random Walk](#random-walk)
* [Respawn](#respawn)
* [Screen](#screen)
* [Script](#script)
* [Sell](#sell)
* [Set State](#set-state)
* [Set Tile](#set-tile)
* [Take Damage](#take-damage)
* [Take Heal](#take-heal)
* [Target](#target)
* [Teleport](#teleport)
* [Unlock Tree](#unlock-tree)
* [Untarget](#untarget)

### Area Specific

* [Always](#always)
* [Enter Area](#enter-area)
* [Inside Area](#inside-area))
* [Leave Area](#leave-area)

### Player Specific

* [Action](#action)
* [Drop](#drop)
* [Move](#move)
* [Take](#take)

### Skills

* [Skill Tree](#skill-tree)
* [Skill Level](#skill-level)

---

### Action

This node is available both in area graphs and in behavior graphs.

It creates a way to map user commands (send from [screen scripts](../scripting/screen_scripts/)) to a node based action.

If used in area graphs it filters the action parameter to a user command. So if a player executes for example a *Look* command and the action node has *Look* as its action parameter the nodes connected on the right will be executed. For example to send a message to a player with the content of a sign.

In behavior node graphs the action node needs to be in a behavior tree which has the name of the action. It works like this:

* The user sends an action command, lets say *Look* in the [screen scripts](../scripting/screen_scripts/). The node system receives the command and searches for a behavior tree called *Look* for the player. If it finds one, it executes the tree.
* When it encounters an action node in the tree it performs the action (which should be *Look* again).

Now the action node does the following:

* It searches for other characters in the direction of the command, if there is a character it searches for a tree with the action name and the ending *(P)*, in our case **Look (P)** and executes the tree if it finds one. The *(P)* indicates that this is a [passive](../../creator/graphs_scripts/mechanics/) tree and gets called from somebody looking at the character. In this tree you can for example send a message to the player using the [message](#message) node (or anything else depending on the action).

* If there is no character, the action node searches for areas in the command direction. If it found one it searches for an action node with a fitting action parameter (as described above, in our case *Look*) and executes it.

In summary, using the *Action* node you can connect any kind of user action to behavior trees on characters or areas, opening up endless possibilities of user interactions with characters and areas.

#### Parameter

* **Action**. The name of the user command

---

### Always

**This node is available only in area graphs**

It makes sure that the connected nodes on the right of the node are always executed, i.e. on every game tick.

A use case for example would be to create a light source using the [Light](#light) node which is always on.

---

### Audio



---

### Call Behavior

Executes the behavior tree of the given name.

#### Parameter

* **System Name**. The name of the system.
* **Tree Name**. The name of the behavior tree in the system to execute.

---

### Call System

Executes a behavior tree of the given system.

#### Parameter

* **System Name**. The name of the system to execute. *Note* that Eldiron checks if this is a variable name and if yes uses the content of the variable instead of given name. This allows to call class specific trees.
* **Tree Name**. The name of the behavior tree to execute.

#### Returns

* **Success**. The system was called successfully.
* **Failure**. The system / tree was not found.

---

### Behavior Tree

A behavior tree is a node with several terminals at the bottom which get executed from left to right. You typically rename the behavior tree to indicate what behavior the tree is executing, for example *Go Raiding*, or *Talk* and *Combat*.

In a programming language behavior trees would be similar to callable functions.

Every behavior tree node has an *Execute* property which indicates when the tree is executed:

- **Always**. The behavior tree is always executed if the graph is not locked.
- **On Startup**. The behavior tree is only executed once when the graph is created.
- **On Demand**. The behavior tree is executed on demand.

Behavior trees perform the AI for non-player-characters (NPCs) and connect input commands from the *Player* character to the right player action.

All behavior trees in a graph are listed as tabs at the top of the graph. Select the given behavior to edit it.

---

### Close In

Intended for NPCs.

Walks towards the current target.

#### Parameters

* **To Distance**. The desired distance to the target. This is most often the weapon range. For a melee weapon it would be 1.
* **Speed Delay**. A numerical expression indicating the walking speed. 0 is the fastest, no delay, the character will move one tile per game tick. Higher values will slow the character down. A value of 4 for example would mean that the character needs 4 game ticks to move to the next tile.

#### Returns

* **Success**. If we have reached the desired distance.
* **Failure**. We are not close enough yet.

---

### Deal Damage

Deals damage to the target.

This node does not deal damage by itself. It just calculates the attack rating, gets the weapon damage and calls the **onHit** tree of the target, which should contain the [Take Damage](take_damage.md) node, which will either block the attack or reduce the damage based on the character attributes of the target.

#### Parameters

* **Attack Rating**. This numerical expression defines the attack rating of the attack. Like ```STR + d3```. The result of this expression will be set as "attack_rating" variable on the target. In the *onHit* tree of the target you can optionally test this variable to see if the character can block the attack.

#### Returns

* **Success**. If we killed the target.
* **Failure**. The target is still alive.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Drop Inventory

Drops all or some of your inventory, making it available for pick up by others. This can be used for example on death.

#### Parameters

* **Drop**. *Everything* will drop the complete inventory and all gold. Whereas *Random Item* will drop a random item and a random amount of gold.

#### See also

[Character Scripts](../scripting/character/)

---

### Drop

**This node is intended for player controlled characters only**

The player character drops the user defined item.

#### Returns

* **Success**. The character dropped the item successfully.
* **Failure**. Failure in dropping the item.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Effect

Plays an effect on the character tile. Mostly used for visualizing taking damage or healing.

#### Parameters

* **Effect**. A tile animation marked as Effect.

---

# Enter Area

**This node is available only in area graphs**

Executes the tree if a character enters the area.

#### Parameter

* **Character**. Either *Everyone* which executes the connected nodes every time a character enters the area or *First Only* which executes the nodes only for the first character to enter the area.

---

### Expression

Executes the given script which is expected to return a boolean value.

#### Returns

* **Success**. If the expression returns ```true```.
* **Failure**. If the expression returns ```false```.

#### See also

[Scripting](../../creator/graphs_scripts/scripting/)

---

### Has State ?

Checks the current state of the character.

 #### Returns

Success if the character currently is of the given state, failure otherwise.

---

### Has Target ?

Intended for NPCs.

 #### Returns

Success if the character currently has a target, failure otherwise.

[Untarget](#untarget)), [Lookout](../nodes/#lookout)

---

### Heal

Heals the current target.

This node does not heal by itself. It just calculates the amount of healing and than calls the **onHeal** tree of the target, which should contain the [Take Heal](#take-heal) node which applies the healing and to optionally increase the healing based on the attributes of the target character.

#### Parameters

* **For**. Either *Self* or *Target*.
* **Amount**. This numerical expression defines the amount of healing. Like ```d10```.
* **Speed Delay**. A numerical expression indicating the delay. 0 means you can heal for every game tick, 4 would mean a possible heal every 4 game ticks.

#### Returns

* **Success**. If we healed the target.
* **Failure**. The healing failed.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Inside Area

**This node is available only in area graphs**

Executes the tree if any character is inside the area.

---

### Leave Area

**This node is available only in area graphs**

Executes the tree if a character leaves the area.

#### Parameter

* **Character**. Either *Everyone* which executes the connected nodes every time a character leaves the area or *Last Only* which executes the nodes only for the last character to exit the area.

---

### Light

This node is available both in area graphs and item graphs.

If executed it creates a light source for the area or the item.

---

### Linear

---

### Lock Tree

---

### Lookout

Intended for NPCs.

This node looks out for other characters to make it the target for an action. For example a monster may look for something to attack, a healer may look out for somebody to heal.

If the node successfully finds a character it will make the character the target, meaning that nodes which work on a target, like [Close In](#close-in), [Deal Damage](#deal-damage) or [Heal](#heal), will target that character.

You can use [Untarget](#untarget) to un-target it again.

#### Parameters

* **State**. You can select if the node looks out for a *Normal* (i.e. active / alive character) or a *Killed* one (for example to resurrect it).
* **Expression**. A numerical expression which checks the potential target character (i.e. this expression is run on the potential target!). For example a monster could check the alignment: ```alignment > 0```.
* **Max Distance**. The maximum distance to look out for characters.

#### Returns

* **Success**. If a fitting character has been found and is our new target.
* **Failure**. If no character has been found.

#### See also

[Untarget](#untarget), [Has Target ?](#has-target)

---

### Message

This node sends a message to the player (or broadcasts a message from the player) and is probably one of the most used nodes.

There are several different message types:

* **Status**. This sends a message to the player from the system and is used for any kind of status updates.

When sending messages there are several kind of codes you can use which the system replaces with the given text.

* ```${CONTEXT}```. The name of the current context, which can either be a character or an item name depending on the node context.
* ```${DEF_CONTEXT}```. The name of the current context of the action prepended by an definite article if appropriate. The name will be in lowercase. For example ```"You take ${DEF_CONTEXT}"``` can become *"You take the torch"*.
* ```${TARGET}```. The name of the current target of the character.
* ```${DEF_TARGET}```. The name of the current target of the character prepended with by a definite article. The name will be in lowercase. For example ```"You kill ${DEF_TARGET}"``` can become *"You kill the orc"*.
* ```${DAMAGE}```. If the character is currently dealing damage to the target or receiving damage, this code will be replaced with the amount of damage dealt or taken.
* ```${HEALING}```. If the character is currently healing the target or receiving healing, this code will be replaced with the amount of healing.

---

### Move

**This node is intended for player controlled characters only**

The node moves the player character in the user specified direction.

#### Parameters

* **Speed Delay**. A numerical expression indicating the walking speed. 0 is the fastest, no delay, the character will move one tile per game tick. Higher values will slow the character down. A value of 4 for example would mean that the character needs 4 game ticks to move to the next tile.

#### Returns

* **Success**. The character moved successfully.
* **Failure**. The path is blocked.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Multi Choice

---

### Pathfinder

Intended for NPCs.

This node finds and walks the path to the given target location or area.

#### Parameters

* **Destination**. The destination position or area. If an area a random position inside the area is choosen.
* **Speed Delay**. A numerical expression indicating the walking speed. 0 is the fastest, no delay, the character will move one tile per game tick. Higher values will slow the character down. A value of 4 for example would mean that the character needs 4 game ticks to move to the next tile.

#### Returns

* **Right**. If the operation is ongoing, i.e. the character did not reach the destination yet, the right terminal is executed.
* **Success**. The character reached the destination.
* **Failure**. If the path to the destination is blocked for a longer period of time.

#### See also

[Random Walk](#random-walk)

---

### Random Walk

Intended for NPCs.

This node randomly walks around the given position or area.

#### Parameters

* **Max Distance**. The maximum distance to walk from the starting position.
* **Speed Delay**. A numerical expression indicating the walking speed. 0 is the fastest, no delay, the character will move one tile per game tick. Higher values will slow the character down. A value of 4 for example would mean that the character needs 4 game ticks to move to the next tile.
* **Delay**. A numerical expression indicating the delay between movements, i.e. how many game ticks the character will wait on the same tile before moving randomly to the next one. 0 means no delay.

#### See also

[Pathfinder](#pathfinder)

---

### Respawn

Intended for NPCs.

Respawns the NPC after a given amount of in-game minutes. Should be applied only to characters which were previously *purged* via [Set State](#set-state).

#### Parameters

* **Minutes to Wait**. The amount of server minutes to wait before respawning.

##### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Screen

**Only available inside the [game view](../game.md)**

Screen nodes define a [screen script](../scripting/screen_scripts/). Screen scripts define what you see on the screen. Games will contain several screen nodes to display various states of the game.

#### Parameters

* **Script**. The screen script.

---

### Schedule

This node checks for a given time period.

#### Parameters

* **From**. The start server time.
* **To**. The end server time.

#### Returns

If the current server time is between the given parameters it will continue with the connection on the right side (i.e. the schedule is in progress.)

Otherwise it will continue with the bottom connection.

---

### Script

Executes the given script.

### See also

[Scripting](../../creator/graphs_scripts/scripting/), [Scripting Reference](../scripting/).

---

### Sell

---

### Sequence

---

### Set State

Sets the state of the character.

* **Normal**. Character is in a normal state.
* **Killed**. Character is killed (and can be resurrected).
* **Purged**. Character is killed and purged from the system (only applies to NPCs).
* **Sleeping**. Character is sleeping.
* **Intoxicated**. Character is intoxicated.

---

### Set Tile

---

### Skill Level

Defines a skill level. Has to be attached to a skill level chain. Rename the node to reflect the skill level you want to implement.

### If this node is used in *Systems / Skills*:

It defines a skill level of a skill, i.e. how many times the skill has to be used to reach the next level (and the name of the levels).

### If this node is used in an *Item*:

It defines the property and speed values for each level of the skill.

#### See also

[Skill Tree](#skill-tree)

---

### Skill Tree

Defines a skill. Rename the node to reflect the skill you want to implement.

### If this node is used in *Systems / Skills*:

It will define a new skill. The [Skill Level](#skill-level) nodes attached to the skill tree define the different levels of the skill. I.e. how many times the skill has to be used to reach the next level (and the name of the levels).

### If this node is used in an *Item*:

It defines which skill the item will increment on use and the property and speed values for each level of the skill.

#### See also

[Skill Level](#skill-level)

---

### Take Damage

Take damage dealt by the [Deal Damage](#deal-damage) node.

This node calculates the reduction of the damage and applies it.

#### Parameters

* **Reduce By**. This numerical expression defines the reduction of the incoming damage.

#### Returns

* **Success**. If the character survives the damage it took.
* **Failure**. The character died. You should now [set the state](#set-state) to *Killed* or *Purged*. See [[Mechanics](../../creator/graphs_scripts/mechanics/). You can [Respawn](respawn.md) non-player characters too.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Take Heal

Heal the amount defined by the [Heal](#heal) node.

This node calculates a potential healing increase and applies it to the hit points.

#### Parameters

* **Increase By**. This numerical expression define the increase of the healing based on character attributes.

#### Returns

* **Success**. The character was successfuly healed for the given amount.
* **Failure**. Healing failed.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Take

**This node is intended for player controlled characters only**

The player character targets tries to take an item in the user specified direction.

#### Parameters

None

#### Returns

* **Success**. The character picked an item up successfully.
* **Failure**. The character cannot pick up anything in this direction.

#### See also

[Mechanics](../../creator/graphs_scripts/mechanics/)

---

### Target

**This node is intended for player controlled characters only**

The player character targets another character in the user specified direction. Nodes like [Deal Damage](#deal-damage) will work on the specified target character.

#### Returns

* **Success**. The character has been successfully target.
* **Failure**. Failure to target.

#### See also

[Mechanics](../nodegraph/mechanics.md

---

### Teleport

---

### Unlock Tree

---

### Untarget

Intended for NPCs.

This node un-targets the current target if the conditions are met.

*Parameters*

* **If Distance is Greater**. Un-target the target if the distance to the current target is greater than the numerical expression. If you always want to un-target enter 0.

*Returns*

* **Success**. We successfully un-targeted the target.
* **Failure**. We did not un-target. We still have a target.

*See also*

[Lookout](#lookout), [Has Target ?](#has-target)

