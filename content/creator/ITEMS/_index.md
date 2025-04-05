---
title: "Items"
weight: 3
description: "Eldiron Creator: Items"
---

## Creating and Editing Items

Creating and editing **items** in Eldiron works **just like** working with [Characters](/creator/CHARACTERS/).

### How to Create an Item
1. Click the **+** button in the [Item](/creator/sections/#item) section.
2. Edit its **behavior** using the **Code Tool**.
3. Set its **attributes** using the **Data Tool**.
4. Drag the item into the **map** to create an **instance**.

> **Important:**
> Make sure to read the [Characters](/creator/characters) chapter, as items share many of the same principles, including scripting and event handling.

## Item Events

Items receive **System and User events** in the same way as characters.

### Example Events:
- If a **player bumps into an item**, the item receives the **`bump_player`** event.
- If the **user clicks an item**, the item receives the **`click`** event.

This makes items **highly flexible**, allowing them to interact with the **map and characters** in different ways depending on the **game style** you are creating.

## Learn More

See the **[Scripting & Data Reference](/scripting_data)** for a complete list of available **events, commands, actions, and data properties**.
