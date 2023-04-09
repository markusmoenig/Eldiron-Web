+++
title = "Region"
weight = 1
alwaysopen = false
+++

In the settings you can tune many region specific settings.

```rust
// The background color of the region
background = #000000
```

A hex color used as the background color of the region while drawing. Default is #000000, i.e. black.

```rust
// Use "tile" for tile based movement or "pixel" for sub-tile movement.
movement = "pixel"
```

Defines the movement mode, tile based movements directly moves characters from one tile to the next, while pixel based movements create a smooth animation between tiles.
```