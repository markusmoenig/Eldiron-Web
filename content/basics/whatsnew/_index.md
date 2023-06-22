---
title: "What's New"
weight: 1
---

### v0.8.2 (2023-6-22)

Mostly a maintenance release.

New Features

* Scrollbars for the node lists, tile-map view and tile-selection view.
* The character position dialog now has an overview map you can use for fast scrolling.

Bugfixes

* User reported bugfixes related to regions and the character position dialog.

### v0.8.1 (2023-6-16)

Some bugfixes and adjusted some script functions to make the API more coherent.

Better Xcode integration.

### First YouTube Video: An Overview of Eldiron (2023-6-15)

{{< youtube FqTC6Yp8tOk >}}

### v0.8.0 (2023-6-1)

Eldiron Creator v0.8.0 for Windows and Linux (.deb) is now live at https://github.com/markusmoenig/Eldiron/releases/tag/v0.8.0. macOS version as always via [TestFlight](https://testflight.apple.com/join/50oZ5yds).

The AUR package is also updated at the usual link: https://aur.archlinux.org/packages/eldiron-bin

v0.8.0 finally (after 2 rewrites) fixes the node and scripting subsystems. It was a bit of a challenge to work this one out. Rust is a great development language but it does not allow sharing memory between tasks easily, and creating an environment which runs full speed and full featured both in Rust / node space and in script space was a bit of a challenge. But the good news is that this is now taken care of and now I can just expand the system with new features easily. And the upside of Rust is that memory runtime bugs are mostly a thing of the past, the old demo is still running on the server w/o ever crashing or loosing memory.

Apart from the rewrite, new things include:

* Basic procedural dungeons. Right now these are not automatic (i.e. dungeons will not be auto generated when you enter them) but I can add this later. The Estartes dungeon was created via the new procedural system. I will expand this system in the next releases to be automatic but also to provide more flexible tile decorations (right now its only one floor / wall tile) and auto monster placements and so on.

* The rewrite provided much more flexibility in item states management, like igniting torches, creating lockable gates (get the key from the orc to unlock the gate in the fortress).

* Completely new and more flexible character sheet system which makes it much more easy to calculate damage based on the character and target character sheets. This is not fully worked out yet, like no saving throws and stuff like this, but this is easy to add now.

* Inheritance. Your characters (both player and NPCs) can now define which class and race they are (like a human fighter). Character behavior trees inherit their behaviors from these systems (race and class) and you just need to implement the trees which are different for your character. For example the Orc in the fortress which carries the key just inherits all behavior from the Orc system class and the startup tree just adds the key to his inventory.

* GitHub Actions is new used to  build new releases for Windows and Linux automatically. The Windows release also features a new .msi installer. All this was contributed by @fionle! Thank you very much! The Mac / iPad builds are still done manually via Xcode.

#### v0.7.5 (2023-3-18)

A new pre-release is available now [here](https://github.com/markusmoenig/Eldiron/releases/tag/v0.7.5).

* Many new features, including an optional raycaster for dungeons.
* A **.deb** binary for Linux.

Any feedback is welcome.

#### Development Update (2023-2-4)

* The region editor now has a preview mode which shows all active elements like character / loot instances and lighting.
* The preview now also works in 3D (although with missing features).
* The tile layers 1-3 have been renamed to F(loor), W(all) and C(eiling), so if you draw the tiles into the correct layers, regions can be displayed both in 2d and 3d. In 2d the tiles are just draw on top of each other while in 3d they are used for the floor / walls / ceiling.
* The O(verlay) layer replaces all tiles in 2d and the wall tiles in 3d (to optionally change the map, reveal hidden passages etc).

The 3d mode still has missing features, like smooth player / monster movements, ceiling support and more. I will implement them over time.

---

#### v0.7.0 (2022-11-2)

First Public Pre-Release

---

#### Started Eldiron Development (2022-1-1)

Another journey begins