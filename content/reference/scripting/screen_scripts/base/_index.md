+++
archetype = "chapter"
title = "Base Classes"
weight = 1
+++

Screen scripts utilize a number of base classes.

### pos

A position on the screen constructed by its x, y coordinates. 0, 0 is the top left corner.

```rust
this.p = pos(20, 30);
```

### rect

A rectangular area on the screen, constructed by its x, y, width and height values.

```rust
self.title_rect = rect(20, 200, 200, 40);

// Test if a position is inside the rect
if self.title_rect.is_inside(p) {
    // inside
}
```

### rgb

A RGB color value, constructed from its red, green and blue components.

```rust
// Color values between 0..255
self.color= rgb(200, 120, 32);
```

