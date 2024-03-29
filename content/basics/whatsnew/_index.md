---
title: "What's New"
weight: 1
---

### Eldiron v0.8.8 and Video (January 21st, 2023)

Eldiron v0.8.8 is now available on [GitHub](https://github.com/markusmoenig/Eldiron/releases).

Here is a short video about the new concepts in the new codebase.

First, when I select a character instance, you see the visual, grid based scripting language which I wrote for Eldiron which I call CodeGridFX. You can visually see how the values change as the server is running. The NPC moves around based on a pulse counter, the player character moves on keyboard based input.

The other new concept is that Eldiron Creator is now build from the ground up for live editing. Meaning you can play your game while you create it. When I change the region by drawing wall tiles, the NPC becomes trapped, when I remove them via Undo, the NPC can move again. This will make it a fun way to create your game interactively while you play it (or you play it while you create it ?).

{{< youtube hrhmtCG9ePw >}}

---

### First Eldiron Test Release (January 12th, 2023)

The first early test release for the new code base (v0.86) is available on  [GitHub](https://github.com/markusmoenig/Eldiron/releases).

This release has many missing features and is not yet ready for production use. It is meant for testing and feedback only.

---

![CodeGrid](./codegrid1.png?classes=left)

### Eldiron Rewrite: Visual Scripting (December 12th, 2023)

**I'm excited to share the latest update for my RPG Creator, featuring the introduction of CodeGrid, a new visual programming language.** CodeGrid seamlessly blends script and node systems, offering a user-friendly drag-and-drop interface.

*One significant challenge with the old Eldiron node system was its lack of flexibility.* While user-friendly, I had to make extensive internal modifications to Eldiron for optimal functionality.

Now, Eldiron's visual scripting UI revolutionizes how it operates. Everything, from character behavior to rendering, effects, and game systems, will be implemented in this language. This transforms Eldiron into a fully flexible sandbox environment. Users can start with default systems and code, adjusting them over time, or they can completely rewrite the system, diverging from Eldiron's standard setup.

**Key Advantages Include:**

1. **Ease of Use**: The system maintains the user-friendly nature of the previous node system, yet offers 100% programmability.
2. **Debugging**: The scripts run visually within the editor during gameplay, allowing real-time verification of every variable and function, with immediate feedback on the map. This feature promises to be incredibly effective.
3. **Speed**: Preliminary indications suggest the new system will significantly outpace the old scripting system. It generates native code compiled by the compiler (via arrays of inlined closures), a method quicker than both AST-based scripting and bytecode-based VMs. This efficiency makes it suitable for complex tasks like writing a visual effects pipeline.
4. **Flexibility**: There are no inherent limitations - Eldiron is a fully-featured sandbox.
5. **Nodes**: While nodes will still be used for certain applications, such as the rendering pipeline, they are now fully programmable with the scripting language. This allows for the use of existing material/rendering nodes or the creation of custom systems.
6. **Screens/Widgets**: Visual UI elements can be linked to visual scripting snippets, simplifying UI design for your game.

*I'll soon demonstrate how the system operates within Eldiron.*

---

### Rewrite of the Creator in Progress (2023-9-6)

After v0.8.4 I decided to rewrite the Creator part of Eldiron.

While I was very happy with the underlying systems, especially the heart of it all, the behavior node system, I was not happy with the UI of the Creator itself.

The Creator was too disjointed. It is logically structured into different sections but it is not productive (or fun) to create behaviors for characters or items “blind” without connection to their usage in the map / game.

I am currently redoing the Creator with a heavy focus on being map centered, i.e. you create the game interacting with items on the map with live previews / gaming and debugging for every single item.

I think this will make for a much more fun experience as you develop the game interactively on the map instead of developing each item in a vacuum.

The current release still contains the old Creator, while v0.9.0 with the new creator is targetted to be released at the end of 2023.

### v0.8.2 (2023-6-22)

Mostly a maintenance release. Scrollbars and fast navigation for regions have been added to all views where necessary. On some Linux systems Rusts winit does not support device scroll events, making it necessary to have scrollbars as fallback.

New Features

* Scrollbars for the node lists, tile-map view and tile-selection view.
* The character position dialog now has an overview map you can use for fast navigation.

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
