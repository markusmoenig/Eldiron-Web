---
title: "SECTOR"
weight: 4
description: "Eldiron Creator: Sector Tool"
---

The **Sector Tool** (keyboard shortcut **'E'**) allows you to **select, edit, and delete sectors** in the map.

Unlike the **Selection Tool**, which can select multiple types of geometry at once, the **Sector Tool** is specifically designed for working with **sectors only**. Unlike the **Linedef Tool**, it does not include a creation mode, as sectors are automatically formed when a closed shape is created.

## Selection Modes

- **Click**: Select a sector.
- **Shift + Click**: Select multiple sectors.
- **Alt (Mac: Option) + Click**: Remove sectors from the selection.
- **Click + Drag**: Move selected sectors.
- **Click + Drag (Empty Area)**: Select a rectangular area of sectors.
- **Delete Key**: Remove selected sectors.
- **Escape Key**: Clear the selection.

Sectors define **floors, ceilings, and traversable areas** in your map. They are automatically created when a **closed polygon** is formed using the **Linedef Tool**.

## Assigning Tiles

You can **assign tiles** to selected sectors to decorate **floors** and **ceilings** by applying a **source** (a tile, material, or color) to the selected surface.

### How to Apply or Remove Tiles:
1. **Select a sector** or **multiple sectors** using the **Sector Tool**.
2. Click the **floor or ceiling icon** in the **HUD** to choose the target surface.
3. Click **Apply** to assign the selected source or **Remove** to clear it.

This allows you to easily customize the look of your game’s floors and ceilings.
