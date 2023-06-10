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

```rust
let sheet = get_sheet();

// Add an item to the inventory
inventory_add(sheet, "Torch");

```