+++
title = "Client Side"
weight = 2
alwaysopen = true
+++

Scripting for the client side is done via screen scripts. See the [Screen](../../nodes/_index.md#screen) node in the Game view. Screen scripts basically draw the contents of the current screen of the game and send commands to the server based on user actions.

### Basics

```rust
// pos, a position on the screen constructed by its x and y coordinates. 0, 0 is the top left corner.
let p = pos(20, 30);

// rect, a rectangular area on the screen, constructed by its x, y, width and height values.
let title_rect = rect(20, 200, 200, 40);
// Test if a position is inside the rect
if title_rect.is_inside(p) {}

// An RGB color value, constructed from its red, green and blue components.
let color = rgb(200, 120, 32);

// An RGBA color value, constructed from its red, green, blue and alpha components.
let color = rgba(200, 120, 32, 128);
```

### Drawing

Eldiron installs a ```tilemaps``` interface in the script context. You can request a specific tile-map by calling the ```get``` function. The name of the tile-map is the same as in the asset view of Eldiron Creator.

```rust
// Get a tile-map
let tm = get_tilemaps().get("Icons");
```

You can get a specific tile from the tile-map using its ```get_tile``` method. It takes the tiles grid location as arguments. You can see the grid locations in the screen editor.

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

