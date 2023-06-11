+++
title = "Server Side"
weight = 1
alwaysopen = true
+++

Server side scripts are arguments for behavior nodes, like the [Script](../../nodes/#script) node.

These scripts define how much damage you deal to another character, or maybe you want to add an item to a character. All this and more can be done easily with server side scripts.

The following script commands work in all nodes.

## Rolling dice

```rust
// Returns a random number between 1 and 6. Works with every number, d18, d1000 etc.
let random_number = d6;

// Rolls a d6 dice 3 times and adds a 2 as modifier. The leading 'r' is required.
let roll = r3d6+2;
```

## Currency

By default the currency in Eldiron is gold and silver, where 10 silver is one gold. I may add more types of coin (platinum, bronze) later but this will not affect the below examples.

```rust
// Create money: 8 gold and 2 silver.
let coin = currency(8, 2);
```

The currency struct is a container only, but you can get a string representation. Use the below sheet functions to add or remove money.

```rust
// "8G 2S"
let string = coin.to_string();
```

## Character Sheets

Every character, if its a player character or an NPC, has its own character sheet. The sheet holds all character info, not only the abilities and hit points but also inventory, equipment, skills, spells etc.

```rust
// Get a copy of the sheet of the current character
let sheet = get_sheet();

// Set a character ability, for example on character creation
sheet.set_ability("STR", r3d6);

// Get the ability
let STR = sheet.get_ability("STR");

// Get / set the max_hit_points for the character
sheet.max_hit_points = 18;
let mhp = sheet.max_hit_points;

// Get / set the hit_points for the character
sheet.hit_points = 18;

// Get / set the wealth of the character
sheet.wealth = currency(8, 2);

// Get the name, class and race names of the character (Defined via the character settings)
let name = sheet.name;
let class = sheet.class;
let race = sheet.race;

// Get / set the alignment of the character
let alignment = sheet.alignment;

// After changing the sheet you have to copy it back to the character
set_sheet(sheet);
```

## Inventory

The inventory is part of the character sheet. Normally you only need to add / remove items manually during character creation. As trading / buying / dropping items is done automatically via the node system.

```rust
let sheet = get_sheet();

// Add an item to the inventory, we get the changed sheet back
sheet = inventory_add(sheet, "Torch");

// Equip an item in the inventory (armor or weapon), we get the changed sheet back
sheet = inventory_equip(sheet, "Sword");

// Get the inventory from the sheet
let inventory = sheet.inventory;

// Iterate over the items of the inventory
for item in inventory {

    // The name of the item
    print("item name: " + item.name);

    // The item amount (for stackable items)
    print("item amount: " + item.amount);

    // The skill tree of the item
    print("Use skill: " + item.use_skill);

    // The current tile of the item
    print("Tile: " + item.tile);

    // The value of the item in currency
    print("Value: " + item.value);
}

// Iterate by index
for index in 0..inventory.len() {
    let item = inventory.item_at(index);
}

// Check if we have an item of the given name
if inventory.has_item("Mandrake") {}

// Destroy an item of the given name, useful for example in crafting
if inventory.destroy_item("Mandrake") {}

// Dont forget to set the sheet back
set_sheet(sheet);
```

## Managing Wealth

```rust
let sheet = get_sheet();

// Add one gold to the wealth of the character
sheet = inventory_add_gold(sheet, 1);

// Add two silver to the wealth of the character
sheet = inventory_add_silver(sheet, 2);

// Add one gold and two silver to wealth of the character
sheet = inventory_add_gold_silver(sheet, 2, 1);

// Dont forget to set the sheet back
set_sheet(sheet);
```

## Increasing experience

When you successfully killed an enemy, or otherwise completed an objective you may want to increase the characters experience by a certain amount.

```rust
let sheet = get_sheet();

// Increase the experience by 10
sheet = increase_experience_by(sheet, 10);

// Dont forget to set the sheet back
set_sheet(sheet);
```

## Target Sheets

When you have a target, which for players is acquired via the [Target](../../nodes/#target) node and for NPCs via the [Lookout](../../nodes/#lookout) node, you can also request the target characters sheet.

```rust
// Get the target sheet
let target_sheet = get_target_sheet();

// Modify ...

// Set the target sheet back
set_target_sheet(target_sheet);
```

In combat you would calculate the damage you deal, get the saving throws and AC from the target and reduct the computed damage from the targets hit_points.

Upon death of the target (if hit_points are equal to 0) you can execute a behavory tree on the target which takes care of the death scenario, see below.

## Executing Behavior

You can execute a behavior tree on the character (or its target) from your scripts:

```rust
// Execute a tree by its name.
execute("MyTree");

// Execute a tree on the current target, for example to handle its death
execute_on_target("onDeath");
```

## Computing Damage

There are various convenience methods available to help you compute the damage the character deals.

```rust
let sheet = get_sheet();

// This function does the following:
// 1. It gets the weapon item in the "main hand" slot
// 2. It looks up the skill tree of the weapon
// 3. It retrieves the damage roll from the skill tree for the characters skill level
// 4. It rolls the damage
let damage = roll_weapon_damage(sheet, "main hand");

// After reducing the damage, based on the targets AC and saving throws, if there
// is damage left, reduct it from the targets hit_points and call
execute_weapon_effects();
// To visually show the damage (tile effect, audio).

// You should also call "increase_skill_by" on the weapon item skill, see below.
```

## Managing Skills

After successfully using an item (like a weapon), you should increase the skill as defined by the items skill tree.

```rust
let sheet = get_sheet();

// Get the skill tree for the given weapon.
let skill_name = get_item_skill(sheet.weapons.slot("main hand"));

// Increase the skill by 1
sheet = increase_skill_by(sheet, skill_name, 1);

// However, for weapons there is a short cut, you can just use
sheet = increase_weapon_skill_by(sheet, "main hand", 1);

// Set the sheet back
set_sheet();
```

## Sending Messages

You can send messages to both the character and its target.

```rust
// Send a status message to the character
send_status_message("You are feeling powerful!");

// Send a status message to the target of the character
send_status_message_target("Shabby crushed you!");
```