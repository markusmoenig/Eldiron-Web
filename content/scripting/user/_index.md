+++
title = "Client: User Related"
weight = 3
alwaysopen = true
+++

When you use Eldiron as an online game, there are some user related script commands you should be aware of. These commands handle the general user management (login, create user, enter games etc.).

However some commands are also useful for local games, like listing the users characters, displaying errors etc.

All these commands work on the client side, within your screen script.

```rust
// If not empty the string will contain a user related error message from the server.
// For example "Wrong Password", "User already exists" etc.
let error_message = get_error_message();

// When logged in (in a local game you are always logged in), returns a list of the users characters
let characters = get_characters();
for c in characters {
    print("Name: " + c.name);
}
```

