+++
archetype = "chapter"
title = "Drawing"
weight = 2
+++

Eldiron installs a ```tilemaps``` interface in the script context. You can request a specific tile-map by calling the ```get``` function. The name of the tile-map is the same as in the [asset view](../assets.md).

```rust
// Get a tile-map
this.tm = this.tilemaps.get("UIParts1");
```

You can get a specific tile from the tile-map using its ```get_tile``` method. It takes the tiles grid location as arguments. You can see the grid locations in the screen editor.

```rust
// Get a tile
this.tile = this.tm.get_tile(13, 1);
```

Eldiron also installs a ```cmd``` interface in the script context which contains all direct action APIs, including the drawing API.

There are various functions available to draw a tile into the screen.

```rust
// Draws a tile using the default size in the given position on the screen.
this.cmd.draw_tile(pos(10, 10), this.tile);

// Same as above but draws the tile in a custom size.
this.cmd.draw_tile_sized(pos(10, 10), this.tile, 40);

// Draws a tile and saturates it with a custom color.
this.cmd.draw_tile_sat(pos(10, 10), this.tile, rgb(100, 120, 80));

// Draws a tile and multiplies it with a custom color
this.cmd.draw_tile_mult(pos(10, 10), this.tile, rgb(100, 120, 80));
```

### Drawing Shapes

