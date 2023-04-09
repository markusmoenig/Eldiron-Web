+++
title = "Eldiron Creator"
alwaysopen = false
weight = 2
+++

Eldiron Creator is a powerful editor for Eldiron game projects.

Under Windows and Linux Eldiron Creator stores its game projects in the *Eldiron* directory of your *Documents* folder.

Under macOS and iOS projects are stored in the iCloud/Eldiron directory, this enables seamless syncinc on these platforms.

Eldiron Creator handles one *Demo Project* and a total of *Four User Projects*. You can seamlessly switch between these projects by just clicking on their icons in the Eldiron Creator toolbar.

* The **Demo** project always contains the latest version of the official demo project for Eldiron. The demo project is meant to be a toolbox for your projects from which you can learn and copy and paste any kind of content into your game projects. **User changes to the demo project are not permanent**. So do not use it to create your game, this is what the user projects are for.

* Create your games by using the **User Projects** only.

### Game Project Folders

Game projects consists of two directories: *assets* and *game*.

##### Assets Directory

The *assets* directory contains all static data of the game.

- The **audio** directory contains all audio assets of your game. Only WAV files are currently supported.

- The **fonts** directory contains all fonts used by the game, to install new fonts just copy new fonts into this directory and on the next restart of Eldiron they will show up in the relevant font selectors.

- The **tilemaps** directory contains all tile-maps. Tile-maps are PNG images which contain game tiles. Copy new images into this folder and they will show up in the **Tiles** view upon restart. Eldiron will create .json files for each tile-map which include the user defined meta data for the tiles.

The name of each file represents the in-game name of the represented entity. For example you can just rename a character file to rename the character itself. Eldiron will perform the same action when asked to rename a character.

##### Game Directory

The *game* directory contains all user created data for the game, such as regions (drawn via tiles in the region editor) or character behavior graphs.

Each folder name represents the type of game content it contains and matches the user interface sections in Eldiron and in this book (i.e. *regions*, *characters*, *systems* and *items*) with the game behavior located directly in the game directory.

You can share individual files with others, but there are some dependencies you have to be aware of:

* *Region* files need the tile-maps used to draw the region in the *assets/tilemaps* directory.

* *Systems* behavior files may be dependent on variables defined in the *characters* which invoke them.

