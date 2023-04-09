+++
title = "Scripting"
weight = 3
+++

Every character (and optionally item) have their own script scopes, so you can create variables and control node flow via expressions.

Scripting is widely used inside Eldiron, as many node parameters are script or expressions. The [Script](../../../reference/nodes/#script) node executes scripts and the [Expression](../../../reference/nodes/#expression) node controls the node flow by either succeeding or failing depending on the boolean return value of the script expression.

Every character should have a startup tree which defines the variables of the character, for example

```rust
let HP = 18 + d2; // 18 plus a dice throw of d2 (a value of 1 or 2)
let HP_MAX = HP;
let STR = 10;
let EXP = 0;
let LEVEL = 1;
...
```

The variables you define make up the attributes of your character. It is up to you if want to create a complex character system or just a minimal one. The example demo project which gets created for a new project is designed to get you started and is not too complex.

The same is true for monsters, you can make them very simple or very complex, the choice is yours. In the early RPGs monsters just had some HP and created random damage. But that was because computers were slow and having a few dozen orcs with fully worked out character systems would have been too slow. This limitation does not exist anymore today.

Apart from character attributes you can of course define as many helper variables as needed.

Note that the ```d2``` dice throw in the example script above is built into the scripting language, you can just use any ```dx``` value (where x is any number) to get a random value between 1 and x (inclusive).

In an [expression](../../../reference/nodes/#expression) node you could check if your character has an experience value greater than 1000 with for example

```rust
EXP > 1000
```

which would follow the green success terminal in the control flow if it is true or the red failure terminal if the character has less than 1000 experience points.

## Special Variables

The node system needs to know which variable name is used for your characters hit points as it needs to check if your character died or not or how much gold it has. These variable names are defined in the [game settings](). When you change one of these special variable names, make sure to change them in all your scripts.

Another special variable is the **alignment** variable. It is set automatically by Eldiron based on your selection for the characters alignment in the character node graph. It is set to 1 for heroes, 0 for neutrals and -1 for monsters. You can of course also use your own more complex alignment system. The alignment is one of the variables often used in the [Lookout](../../../reference/nodes/#lookout) node.

---

For more information about scripting please see the [scripting reference](../../../reference/scripting/), especially the [character scripts](../../../reference/scripting//character/).