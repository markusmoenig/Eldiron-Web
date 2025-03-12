---
title: "CONFIGURATION"
weight: 5
description: "Configuration Reference"
---


## Configuring Eldiron

You can configure **Eldiron** using the **Config Tool** with the in-built **TOML editor**.

---

## Game Configuration

Game configuration options are located in the `[game]` section.

```toml
[game]
target_fps = 30      # The target frames per second for the game.
game_tick_ms = 250   # The milliseconds per game tick.
ticks_per_minute = 4 # The amount of ticks per in-game minute.

entity_block_mode = "always" # The block mode, "always" or "never"
```
### **Option Descriptions**

- **`target_fps`**
  - Defines the **refresh rate** of the game.
  - A **higher FPS** results in **smoother gameplay**, but increases CPU usage.

- **`game_tick_ms`**
  - Sets the **milliseconds per game tick**, which is **Eldiron’s internal clock**.
  - Events, actions, and player interactions are processed **each tick**.
  - Default: `250 ms`, meaning **4 ticks per second** (suitable for most games).

- **`ticks_per_minute`**
  - Defines the **number of ticks per in-game minute**.
  - Default: `4`, meaning **1 in-game minute = 1 real-time second**.
  - To sync in-game time with real time, set this value to **`60 * 4 = 240`**.

- **`entity_block_mode`**
  - Controls whether **entities (i.e., characters)** can move through each other.
  - `"always"` → Entities **always block each other**.
  - `"never"` → Entities **never block each other**.

> [!TIP]
> A future update will introduce **custom entity block modes** to support **alignment-based blocking** and other movement rules.

### **Using In-Game Time for Events**

Some commands use **in-game minutes** for timing.
For example, the `notify_in` command schedules events **after a set number of in-game minutes**:

```python
notify_in(2, "close_door")
```

With the **default settings**, this means the event will trigger **after 2 real-time seconds**.

---

## Render Configuration

Render configuration options are located in the `[render]` section.

```toml
[render]
sample_mode = "nearest" # "nearest" or "linear"
```
### **Option Descriptions**

- **`sample_mode`**
  - Defines the **interpolation mode** used for **scaling textures**.
  - `"nearest"` → **Nearest-neighbor interpolation** (best for pixel art).
  - `"linear"` → **Bilinear interpolation** (better for high-resolution textures).
  - **Recommendation:** Use `"nearest"` for pixel art games to preserve crisp edges.
