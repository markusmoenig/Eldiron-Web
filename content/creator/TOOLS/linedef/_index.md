---
title: "LINEDEF"
weight: 3
description: "Eldiron Creator: Linedef Tool"
---

The **Linedef Tool** (keyboard shortcut **'L'**) allows you to **select, edit, and create linedefs** in the map.

Unlike the **Selection Tool**, which can select multiple types of geometry at once, the **Linedef Tool** is specifically designed for working with **linedefs only**. It also includes a **creation mode** for quickly building map geometry.

## Selection Modes

- **Click**: Select a linedef.
- **Shift + Click**: Select multiple linedefs.
- **Alt (Mac: Option) + Click**: Remove linedefs from the selection.
- **Click + Drag**: Move selected linedefs.
- **Click + Drag (Empty Area)**: Select a rectangular area of linedefs.
- **Delete Key**: Remove selected linedefs.
- **Escape Key**: Clear the selection.

## Creation Mode

- **Click on free space**: Creates a new **vertex**.
- **Click again on another free space**: Creates a **linedef** between the new vertex and the previous one.
- **Clicking on an existing vertex**: Extends the shape by connecting to the selected vertex.
- **Closing a polygon** (by connecting the last linedef to the starting vertex) **automatically creates a sector**.

This tool is essential for constructing walls, paths, and enclosed areas in your map.

## Assigning Tiles

You can **assign tiles** to selected linedefs (for decorating walls) by applying a **source** (a tile, material, or color) to the selected row.

### How to Apply or Remove Tiles:
1. **Select a linedef** or **multiple linedefs** using the **Linedef Tool**.
2. Click the **row icon** in the **HUD** to choose the target row.
3. Click **Apply** to assign the selected source or **Remove** to clear it.

This allows you to easily customize walls and other vertical surfaces in your map.
