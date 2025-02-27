---
title: "SCRIPTING & DATA"
weight: 4
description: "Scripting & Data Reference"
---

## Overview

This chapter serves as a reference for **scripting and data attributes** used in [Characters](/creator/characters) and [Items](/creator/items) in Eldiron.

Since many **events, commands, and attributes** are shared between the two, they are **listed together**, with any **specific differences noted where applicable**.

> [!NOTE]
> This chapter is work in progress.

---

## Setting Basic Attributes

Attributes can be set using **Python (Code Tool)** or **TOML (Data Tool)**.

### **Using Python (Code Tool)**

The attributes can be set inside the templates or the [instance scripts](/creator/characters/#instances) of **characters** or **items**.

```python
# Give the character or item a name (if they differ from the template)
set_name("Orc")
# Set the tile ID for the character or item. Get the tile ID from the tile-picker.
set_tile("tile_id")
# Make the character or item visible / invisible
set_attr("visible", False)
# Change the collision radius for characters and items (default is 0.5)
set_attr("radius", 0.3)

# Item specific

# Make the item blocking / unblocking
set_attr("blocking", True)
# Make the item static (doors, campfires etc.). Static, blocking items have a square collision radius.
set_attr("static", True)

# Setting general purpose attributes
set_attr("STR", 10)
```

### **Using TOML (Data Tool)**

```toml
[attributes]
# Give the character or item a name (if they differ from the template)
name = "Orc"
# Set the tile ID for the character or item. Get the tile ID from the tile-picker.
tile_id = "tile_id"
# Make the character or item visible / invisible
visible = false
# Change the collision radius for characters and items (default is 0.5)
radius = 0.3

# Item specific

# Make the item blocking / unblocking
blocking = true
# Make the item static (doors, campfires etc.). Static, blocking items have a square collision radius.
static = true

# General purpose attributes
STR = 10
```
