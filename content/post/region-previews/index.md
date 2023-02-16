---
title: Region Previews
description: Real previews in the Region Editor
slug: region-previews
date: 2023-02-04 00:00:00+0000
image: cover.png
categories:
    - Development Updates
tags:
    - Development Updates
---

The region editor now has a preview mode which shows all active elements like character / loot instances and lighting.

The preview now also works in 3D (although with missing features).

The tile layers 1-3 have been renamed to F(loor), W(all) and C(eiling), so if you draw the tiles into the correct layers, regions can be displayed both in 2d and 3d. In 2d the tiles are just draw on top of each other while in 3d they are used for the floor / walls / ceiling.

The O(verlay) layer replaces all tiles in 2d and the wall tiles in 3d (to optionally change the map, reveal hidden passages etc).

The 3d mode still has missing features, like smooth player / monster movements, ceiling support and more. I will implement them over time.

![Preview 3D](preview-3d.png)
