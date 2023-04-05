+++
archetype = "chapter"
title = "Screen Scripts"
weight = 1
+++

Screen scripts define the visible content of your game as well as the player interaction. Screen scripts are part of screen nodes in the [game view](./game.md).

Screen scripts consists of several functions which will be called by Eldiron for various tasks:

```rust

fn init() {
    // Initialize your screen script here. "this" is the global context.

    // this.width and this.height are set by default to the game settings screen_size.
    // Default is 1024 x 608.

    // this.tile_size is set to the game settings def_square_tile_size value.
    // Default is 32. Change it here for custom tile sizes.
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
    // The mouse has been pressed or a touch event occured at the specified coords.
}
```

The sub-chapters discuss all of Eldiron's script functions available to you in screen scripts.
