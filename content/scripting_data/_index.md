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

# Make the item blocking (based on its radius)
set_attr("blocking", True)

# Make the item static (doors, campfires etc.). Static items cannot be picked up.
set_attr("static", True)

# Setting general purpose attributes
set_attr("STR", 10)
```

### **Using TOML (Data Tool)**

```toml
[attributes]

# Give the character or item a name (if they differ from the template)
name = "Orc"

# Set the tile ID for the character or item. Get the tile ID from the tile-picker
tile_id = "tile_id"

# Make the character or item visible / invisible
visible = false

# Change the collision radius for characters and items (default is 0.5)
radius = 0.3

# Item specific

# Make the item blocking (based on its radius)
blocking = true

# Make the item static (doors, campfires etc.). Static items cannot be picked up
static = true

# General purpose attributes
STR = 10
```

---

## Available Scripting Commands

### Commands for Both Characters and Items

These commands can be used for both **characters** and **items**:

```python
# Send a debug message to the Log.
debug(arg1, arg2, ...)

# Return the name of the sector the character or item is in.
get_sector_name()

# Send the event string to the character or item after a given amount of in-game minutes.
# By default, one in game minute is one second in real time.
notify_in(minutes, event_string)

# Set an attribute of a character or item. Value can be any Python value.
set_attr("key", value)
```

### Commands for Characters Only

These commands are **exclusive to characters** and are primarily used for **NPC behavior**:

```python
# Loop: Walks the character in a random direction for the given distance and speed.
# After arrival, sleeps for a random amount of in-game-minutes between 0 and max_sleep.
# Example: random_walk(1.0, 1.0, 8)
# Mostly used for NPCs
random_walk(distance, speed, max_sleep)

# Loop: Walks the character to a random position in the current sector for the given distance and speed.
# In between sleeps the character for a random amount of in-game-minutes between 0 and max_sleep.
# Example: random_walk_in_sector(1.0, 8)
# Mostly used for NPCs
random_walk_in_sector(speed, max_sleep)

# Register a player character. Only than do they receive user inputevents from the game.
register_player()
```

### Applying Player Actions

The `action` command is used to trigger **player actions** based on user input.

By default, a character’s `user_event` method looks like this:

```python
def user_event(self, event, value):
    if event == 'key_down':
        if value == 'w':
            action("forward")
        if value == 'a':
            action("left")
        if value == 'd':
            action("right")
        if value == 's':
            action("backward")
    if event == 'key_up':
            action("none")
```

> [!NOTE]
> Player characters must be registered using the `register_player` command.

> [!TIP]
> These movement commands are **camera-independent** and work for **2D, isometric, and first-person cameras**.

### Available Actions

```python
# 2D and Isometric: Move the player north.
# First-Person: Move the player forward in their current facing direction.
action("forward")

# 2D and Isometric: Move the player west.
# First-Person: Rotate the player to their left.
action("left")

# 2D and Isometric: Move the player east.
# First-Person: Rotate the player to their right.
action("right")

# 2D and Isometric: Move the player south.
# First-Person: Move the player backward in their current facing direction.
action("backward")

# Stop any movement / action.
action("none")
```
