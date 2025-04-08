---
title: "Configuration"
weight: 6
description: "Configuration Reference"
---

## Configuring Eldiron

You can configure **Eldiron** using the **Config Tool** with the in-built **TOML editor**.

---

## Game Configuration

Game configuration options are located in the `[game]` section.

```toml
[game]
[game]
target_fps = 30                # The target frames per second for the game.
game_tick_ms = 250             # The milliseconds per game tick.
ticks_per_minute = 4           # The amount of ticks per in-game minute.
entity_block_mode = "always"   # The block mode, "always" or "never".
auto_create_player = true      # Whether to auto-create a player entity.
start_region = ""              # The name of the region to start the game in.
start_screen = ""              # The name of the screen to show at startup.

# Base currency configuration
base_currency_name = "Gold"      # Display name of the primary in-game currency.
base_currency_symbol = "G"       # Symbol used to represent the currency (e.g. "G" for Gold).
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

- **`auto_create_player`**
  If `true`, Eldiron will automatically **create a player instance** in the map if one is defined.
  Useful for quickly testing and building games without needing to implement a full character creation process.
  If `false`, the player must be created manually—typically using a **screen** and **user input flow**.

- **`start_region`**
  The **name of the region** the game will load when it starts.
  If `start_screen` is not set, this first region will be shown by default.

- **`start_screen`**
  The **name of the screen** to load on startup.
  If empty, Eldiron will display a black screen.

#### `base_currency_name`
- The **display name** of your game's primary currency (e.g. `"Gold"`, `"Credits"`).
- Used in the UI, item pricing, and trade.

#### `base_currency_symbol`
- The **short symbol** shown with currency values (e.g. `"G"`).
- Appears alongside numbers (e.g. `50 G`, `100 💎`).

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

---

## Viewport Configuration

Viewport configuration defines the resolution and grid used when the game starts.

```toml
[viewport]
width = 1280        # Width of the game viewport in pixels.
height = 720        # Height of the game viewport in pixels.
grid_size = 32      # Size of one grid tile in pixels.
```

  ### **Option Descriptions**

  - **`width` / `height`**
    Defines the **starting resolution** of the game window or screen.
    You can adjust these values to target common resolutions like 1280×720 or 1920×1080.

  - **`grid_size`**
    Sets the **pixel size of a single tile** in the world/grid.
    This affects rendering and snapping behavior in tools and the viewport layout.
