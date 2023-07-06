+++
title = "Client Side"
weight = 2
alwaysopen = true
+++

Scripting for the client side is done via screen scripts. See the [Screen](../../nodes/_index.md#screen) node in the Game view. Screen scripts basically draw the contents of the current screen of the game and send commands to the server based on user actions.

Screen scripts consists of several functions which will be called by Eldiron for various tasks:

```rust

fn init() {
    // Initialize your screen script here. "this" is the global context.
    this.my_var = 5;
}

fn draw() {
    // Draw the content of the screen
}

fn key_down(key) {
    // Key press event
    if key == "w" {
        // Do something
    }
}

fn touch_down(x, y) {
    // The mouse has been pressed or a touch event occured at the specified coordinates.
}
```

More functions will be added in the future.

You can import other scripts into your main screen script via the import command:

```rust
// Import the "button" script
import "button" as button;

// Access a class in button
this.switch_button = button::TextButton("MODERN", rect(28, 28, 80, 20));
```

## Basics

```rust
// A position on the screen constructed by its x and y coordinates. 0, 0 is the top left corner.
let p = pos(20, 30);

// A rectangular area on the screen, constructed by its x, y, width and height values.
let title_rect = rect(20, 200, 200, 40);
// Test if a position is inside the rect
if title_rect.is_inside(p) {}

// An RGB color value, constructed from its red, green and blue components.
let color = rgb(200, 120, 32);

// An RGBA color value, constructed from its red, green, blue and alpha components.
let color = rgba(200, 120, 32, 128);
```

## Drawing

The name of the tilemaps or images is the same as in the asset view of Eldiron Creator.

```rust
// Get the tilemaps and a reference to the "Icons" map.
let tm = get_tilemaps().get("Icons");
```

You can get a specific tile from the tile-map using its ```get_tile``` method. It takes the tiles grid location as arguments. You can see the grid locations in the asset or screen editor of Eldiron Creator.

```rust
// Get a tile
let tile = tm.get_tile(13, 1);
```

There are various functions available to draw a tile into the screen.

```rust
// Draws a tile using the default size in the given position on the screen.
draw_tile(pos(10, 10), tile);

// Same as above but draws the tile in a custom size.
draw_tile_sized(pos(10, 10), tile, 40);

// Draws a tile and saturates it with a custom color.
draw_tile_sat(pos(10, 10), this.tile, rgb(100, 120, 80));

// Draws a tile and multiplies it with a custom color
draw_tile_mult(pos(10, 10), this.tile, rgb(100, 120, 80));
```

You can adjust use default size a tile is drawn with (which is defined in the game settings) with
```rust
// Override the default tile size
set_tile_size(41);

// Get the current tile size
let curr_tile_size = get_tile_size();
```

Drawing images works similar.

```rust
// Get an image
let logo = get_images().get("eldiron_logo");

// Draws the image with the given width and height and a blend factor.
// 1.0 is full opacity, 0.0 is fully transparent.
draw_image(pos(10, 10), logo, 200, 200, 1.0);
```

You can also request the screen dimensions of the client with

```rust
// Get screen dimensions
let width = get_width();
let height = get_height();
```

Other drawing routines:

```rust
// Draw a rectangle, works with both rgb and rgba colors
draw_rect(rect(215, 2, 180, 25), rgb(0, 0, 0));

// Draw a text at the given position using the specified font name, size, and color.
// The font has to be installed in the Game assets font folder.
draw_text(pos(220, 2), "Eldiron Demo", "Roboto Medium", 19.0, rgb(150, 150, 150));

// Draws the text inside the given rectangle. You can use "left", "center" and "right"
// to align the text horizontally.
draw_text_rect(rect, "Eldiron Demo", "Roboto Medium", 15.0, rgb(180, 180, 180), "center");
```

Drawing game elements:

```rust
// Draws the game messages inside the given rect
draw_messages(rect, "Roboto Medium", 16.0, color);

// Draw the game view in 2d in the given rectangle
draw_game_2d(rect);

// Draws the game view in 2d in the given rectangle and relatively offsets the player
// position bypos_offset. This is useful when the player should not be centered.
// For example in the modern demo the UI on the right side is transparent so we want
// to offset the player position to the left.
draw_game_offset_2d(rect, pos_offset);

// Draw the game view in 3d (using the raycaster) in the given rectangle.
draw_game_3d(rect);
```

The 2d and 3d game drawing calls can be combined, for example you can use the 2d drawing call to create a minimap with a smaller tile size.

However you must tell Eldiron what is the main drawing method as the 3d mode has different input / movement modes.

Use on of the two calls to set the main movement mode for the player, the default is 2d.

```rust
// Set the main input mode to either 2d or 3d with one of these calls.
set_display_mode_2d(true / false);
set_display_mode_3d(true / false);
```

## Sending game commands

The client, based on user input, can send action commands to the server. The server will execute the behavior tree of the same name as the action command. This enables you to map any command to any server character behavior.

```rust
// The action command sends the action and the direction of the action to the server.
// Examples:
action("Move", "North");
action("Attack", "East");

// The action_at_coordinate() command sends the action command but uses the coordinates
// of the latest clicked tile. Use this command if a touch_down() event is inside the
// game rect.
action_at_coordinate("Look");
```

For ```action_at_coordinate``` (or any at_coordinate function) you can set the valid rectangle to check for coordinate based actions. Sometimes you will draw icons on top of your game view and you want to exclude these areas. You can do this using:

```rust
// Only check for mouse based action inside this rect.
set_valid_mouse_rect(rect);
```

## Actions on your Inventory

To execute actions on your inventory (mostly "Look" or "Use" commands etc.), use:

```rust
// Execute the "Use" behavior tree for the inventory item in slot 0
action_inventory("Use", 0);

// Try to equip the item in slot 1
action_inventory("Equip", 1);
```

Note that you do not equip or drop inventory items directly. You call the behavior tree which handles this behavior. The behavior tree would send back status messages informing the user of the outcome of the action.

## Casting spells

Cast a spell in the given direction or location:

```rust
// Cast the "Fireball" spell to the "East".
spell("Fireball", "East");

// Cast the "Fireball" spell at a coordinate.
spell_at_coordinate("Fireball");
```

## Convenience methods

You can request the character sheet via ```get_sheet``` just like on the server, however often in a certain script module you just want to print the available inventory items or gear. To do this use one of the below convenience methods.

```rust
// Get the full character sheet, set_sheet() is not implemented for the client.
let sheet = get_sheet();

// Same as sheet.inventory
let inventory = get_inventory();

// Same as sheet.spells
let spells = get_spells();

// Same as sheet.weapons
let weapons = get_weapons();

// Same as sheet.gear
let gear = get_gear();

// Same as sheet.wealth
let currency = get_wealth();

// Same as sheet.experience
let exp = get_experience();
```

For more information on character sheets see the server scripting documentation. On the client side character sheets are read-only, there is no way for the client to send updated client sheets back to the server.

## Get the current server Date and Time

```rust
// Get the server date and time.
let date = get_date();
```