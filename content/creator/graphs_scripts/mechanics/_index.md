+++
title = "Mechanics"
weight = 4
+++

While the behavior trees are very flexible, there are some fixed mechanics which are important to understand.

## Dealing and Taking Damage

Your character can deal damage via the [Deal Damage](../../../reference/nodes/#deal-damage) node. The amount of damage dealt is specified by the equipped item (and the item level).

However the deal damage node by itself does not do any damage, it will look up and execute the **onHit** behavior tree on the receiving character and execute it. This tree should contain a [Take Damage](../../../reference/nodes/#take-damage) node which has an *Reduce By* parameter which calculates the amount to reduce the incoming damage. This expression can again any bonuses from the character class or gear into account to reduce the damage. After that the node applies the incoming damage (which was reduced by the calculated amount) and applies it to the hit point variable specified in the [game settings]() (*HP* by default).

If the character succeeds to take damage (i.e. does not die which means the hit points are greater than 0) it executes the green success terminal of the take damage node, if the hit points are 0 the red failure terminal is executed. See *Dying and Resurrection* below.

```admonish warning
If a character does not have a ```onHit``` tree or that tree does not have a take damage node, the character will never take damage!
```

## Healing and Taking Healing

The healing process is very similar to dealing damage. The [Heal](../../../reference/nodes/#heal) node is used to specify the amount to heal, it than calls the **onHeal** tree on the receiving character which has to call the [Take Heal](../../../reference/nodes/#take-heal) node to apply the healing.

Similar to the damage system, if a character has no **onHeal** tree or does not call the take heal node it will not be able to receive healing.

## Dying and Resurrection

If the [Take Damage](../../../reference/nodes/#take-damage) node fails it means your character should do. You can set the state of the character via the [Set State](../../../reference/nodes/#set-state) node. Purging the character means it will be deleted from the system. For a player character set it to Killed so that the character is not purged but can be resurrected later.

The example demo teleports the player to a healer who will resurrect him using the set state node. The healer uses the [Lookout](../../../reference/nodes/#lookout) node to find character who can be resurrected. See *Targeting* below.

## Targeting

Players target other characters explicitly by performing some action in a given direction. But how do non player character target other characters ? The answer is the already mentioned [Lookout](../../../reference/nodes/#lookout) node. This node searches all characters in the vicinity and checks if the character fits the expression. You can for example check its *alignment*. The node also allows checking the state of the character (*Normal* or *Killed*). For details please see the documentation of the [Lookout](../../../reference/nodes/#lookout) node.

If the lookout node finds a fitting character, it will set that character as the target. That means that nodes which work on a target, like [Close In](../../../reference/nodes/#close-in), [Deal Damage](../../../reference/nodes/#deal-damage) or [Heal](../../../reference/nodes/#heal), will target that character.

You can un-target using the [Untarget](../../../reference/nodes/#untarget) node (for example if the target is too far away).

## Skills

By adding [Skill Tree](../../../reference/nodes/#skill-tree) nodes to *Systems / Skills*, you can create new skills. These skills can be linked from items to reference which skill to increment on use and which property and speed values to use for each level of the skill.

---

Congratulations, you understood the most complex mechanics in Eldiron!
