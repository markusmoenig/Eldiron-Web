+++
title = "Scripting"
weight = 4
alwaysopen = false
+++

The scripting engine in Eldiron uses [Rhai](https://rhai.rs), a Rust based, easy-to-use yet powerful scripting language. Please see the [Rhai Book](https://rhai.rs/book/) for furher information on Rhai and it's syntax.

There are two kind of scripting systems in Eldiron.

## Server side

On the server scripting is mainly used for character behavior. Although the behavior is mostly handled by behavior trees, many of the arguments of the various behavior nodes are small scripts.

Mostly these scripts are single line or a few lines at most.

## Client side

Client side scripts are called screen scripts, they define and draw the content of the currently displayed screen (window) and send player commands to the server based on user actions.

Client scripts are larger scripts. You can edit them inside Eldiron Creator or use your editor of choice to edit them.

Screens are handled by the [Screen](../nodes/#screen) node in the Game view.