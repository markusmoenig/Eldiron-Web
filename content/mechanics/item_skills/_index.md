+++
title = "Item based Skills"
weight = 5
alwaysopen = true
+++

Eldiron currently supports item based skills, which can be used to roll weapon damage or any other value depending on the items functionality (like for example the block value for a "Shield").

All *Skills* for your game are skill trees located in a special systems object called *Skills*.

![Skill Trees](./skill_trees.png)

Here a *Swords* skill is shown. Each skill needs to start with a [Skill Tree](../../nodes/#skill-tree) node which has several [Skill Level](../../nodes/#skill-level) nodes attached. Each skill level defines the total number of times the skill needs to be used to gain this level and the message to send to the user when the level is reached.

Now items can implement these skills:

![Item Skill Trees](./item_skill_trees.png)

You use the same nodes to implement a skill tree within the item object. However now the skill level represents a script which represents the value for the given skill level (which is the damage for a weapon) and the delay in game ticks when using the skill.

To the right of the skill level you can also assign effects (tile based animations or audio) when the skill is used.

### Using Skills

Skills are used mostly in scripts, there are easy to use convenice methods which are discussed in [server side scripting](../../scripting/server/#managing-skills).

Basically you use

```rust
// Roll the damage for a weapon in the given weapon slot
let damage = roll_weapon_damage(sheet, "main hand");

// or for a general item, use the item name
let result = roll_item_skill("Shield");
```

These functions automatically choose the right skill level based on the skills of the character.

Furthermore you can increase skills on successful use by a certain amount using:

```rust
//For a weapons in a given weapon slot
sheet = increase_weapon_skill_by(sheet, "main hand", 1);

// or for a general skill use the skill name
sheet = increase_skill_by(sheet, "Shields", 1);

// You can get the skill name for an item via
let skill_name = get_item_skill(item);
```

You can play the weapon effects on the target with

```rust
execute_weapon_effects();
```