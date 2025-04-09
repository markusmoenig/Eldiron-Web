---
title: "Screens & Widgets"
weight: 5
description: "Scripts & Widgets"
---

## Overview

**Screens** are special maps that define the **visible area** of your game—typically used for **UI layout**, **menus**, or **HUDs**.

You can design screens using the **same map-based tools** available in Eldiron. Use the **Linedef** and **Sector Tool** to define areas, and name the sectors to turn them into **widgets**.

Each **named sector** becomes a **widget**, and its behavior or appearance can be configured via the **Data Tool**.

Use the **Rect Tool** to draw **visual decorations** or layout elements onto the screen.

---

## Game Widgets

A widget with the role `"game"` is responsible for **drawing the game world** inside a screen.

For **2D games**, you can define the `grid_size` property, which determines the **pixel size of one tile** rendered within the widget.
This effectively sets the **zoom level** of the game view inside the screen.

If `grid_size` is not set, it defaults to the value defined in the global `[viewport]` section.

### Example

```toml
[ui]
# The role of the widget, "none", "game", "button", "text"
role = "game"
grid_size = "40"
```

---

## Button Widgets

**Button widgets** define interactive UI elements that trigger **game actions** or other logic when clicked.

Buttons are **visually styled** using the **tiles** defined in the **Sector Tool**:
- The **default (normal)** state is drawn from the sector’s base tiles.
- The **active** state is shown when the button is clicked or when its associated action is currently active.

---

### Example

In this example, clicking the button causes the player to **move forward**.
(See the list of available actions [here](scripting_data/index.html#available-actions)):

```toml
[ui]
role = "button"
# The action to send to the server when clicked
# See https://eldiron.com/scripting_data/index.html#available-actions
action = "forward"
```

---

## Text Widgets

**Text widgets** display text on the screen and can include **static content** or **dynamic placeholders** for player or game data.

Text is entered in the `text` field using a multiline string. You can insert dynamic values using placeholders like `{PLAYER.STR}` or `{PLAYER.DEX}`, which will be replaced at runtime. `{PLAYER.FUNDS}` gets replaced by the player funds in the base currency.

You can customize the **font**, **size**, **line spacing**, and **color** of the text.

### Example

```toml
[ui]
role = "text"
text = """
Welcome, adventurer!

STR:  {PLAYER.STR}  DEX: {PLAYER.DEX}
GOLD: {PLAYER.FUNDS}

May the stars guide you!
"""

font = "Tiny5-Regular"
font_size = 18.0
spacing = 2.0
color = "#aaaaaa"
```

---

## Messages Widget

The **Messages widget** displays all incoming messages for the player in a scrollable list.

- Messages are sent using the `message` command.
- Each message can include an optional **category**, which determines its **display color**.
- If no category is specified, messages default to color `#aaaaaa`, however you can change this via "default".

You can define custom **colors for categories** using keys in the widget's data section.
In the example below, messages with the `"warning"` category will appear in **light red**.

By default, messages are listed **bottom-up** (most recent at the bottom).
To change this to **top-down**, set `top_down = true` in the widget’s configuration.

### Example

```toml
role = "messages"
font = "Tiny5-Regular"
font_size = 18.0
spacing = 5.0
warning = "#ff8888"
default = "#ffffff"
```
