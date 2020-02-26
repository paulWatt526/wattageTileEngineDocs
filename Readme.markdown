# Wattage Tile Engine: Plugin API Docs

![Wattage Tile Engine Logo](img/logo.png)

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Library](http://docs.coronalabs.com/api/type/Library.html)
| __Keywords__         | Tiles, Tile, Tile Engine, Engine
| __See also__         | 

## Quickstart

Source code may be found from [here](https://github.com/paulWatt526/tileEngine).

Find screenshots of the tile engine in action [here](#screenshots), and a
video of the tech demo [here](#videos).

The Wattage Tile Engine is easy to use.  Check out the quick
start guide [here](quickstart.markdown) to get up and running fast.  Or
download the [template](https://github.com/paulWatt526/wattageTileEngineAppTemplate)
and start your own project.  Be sure to check out the variety of
sample code [below](#sample-code).

## Overview

The wattageTileEngine plugin can be used in your
[Corona](https://coronalabs.com/products/corona-sdk/) project.  It enables
the display of a large number of tiles and includes the following features:

* Support for a large number of tiles.
* Support for very large worlds which are too large to load entirely
into memory through the use of the RegionManager. See the RegionManager
guide below.
* Dynamic lighting effects.
    * Tiles may be configured as opaque to cast shadows.
    * Opaque tiles may be added/removed arbitrarily and their effects
    on shadows will be realized in real-time.
    * Lights may be added and removed arbitrarily and their effects
    are realized in real-time.
    * Ability to specify ambient lighting.  This is useful for outdoor
    scenes.
    * Ability to specify whether a tile is affected by ambient light.
    This is useful for indoor tiles in an outdoor environment.
    * Lights may be moved with smooth transitions between their states.
    * Entities are affected by the lighting in each tile.
* Dynamic line of sight.  Useful for hiding tiles that would not be
visible to the player.
* Dynamic tile definitions.  Useful for representing a dynamic world.
* Multiple layers.
* Multiple layer types (Tile, Entity)
* Parallax scrolling between layers.
* Camera which supports arbitrary viewing positions and different levels
of zoom.

## Guides

* [Quickstart](quickstart.markdown)
* [Lua OOP Primer (Optional)](luaOopPrimer.markdown)
* [ObjectSystem Usage Guide (Optional)](objectSystem/usageGuide.markdown)
* [Creating Very Large Worlds Using RegionManager](regionManager/usageGuide.markdown)

## Syntax

	local wattageTileEngine = require "plugin.wattageTileEngine"

### Libraries

* [ObjectSystem](objectSystem/lib_objectSystem.markdown)
* [Utils](utils/lib_utils.markdown)

### Types

The following types are exposed by the Wattage Tile Engine library:

* [Camera](camera/type_camera.markdown)
* [Engine](engine/type_engine.markdown)
* [EntityLayer](entityLayer/type_entityLayer.markdown)
* [LightingModel](lightingModel/type_lightingModel.markdown)
* [LineOfSightModel](lineOfSightModel/type_lineOfSightModel.markdown)
* [Module](module/type_module.markdown)
* [RegionManager](regionManager/type_regionManager.markdown)
* [SpriteInfo](spriteInfo/type_spriteInfo.markdown)
* [Tile](tile/type_tile.markdown)
* [TileLayer](tileLayer/type_tileLayer.markdown)
* [ViewControl](viewControl/type_viewControl.markdown)


## Project Configuration

Clone the source from:
```
https://github.com/paulWatt526/tileEngine
```
then copy the "plugin" folder into your project.  The library can then be
included using:
```
local wattageTileEngine = require "plugin.wattageTileEngine"
```

## Platform-specific Notes

None.

## Resources

### Sample Code

The template serves as a bare bones example.

* [Template Code](https://github.com/paulWatt526/wattageTileEngineAppTemplate)

The [Quickstart Guide](quickstart.markdown)
walks through all of the following sample code:

* [Quickstart Stage 1 Code](https://github.com/paulWatt526/tileEngineQuickStart1)
* [Quickstart Stage 2 Code](https://github.com/paulWatt526/tileEngineQuickStart2)
* [Quickstart Stage 3 Code](https://github.com/paulWatt526/tileEngineQuickStart3)
* [Quickstart Stage 4 Code](https://github.com/paulWatt526/tileEngineQuickStart4)
* [Quickstart Stage 5 Code](https://github.com/paulWatt526/tileEngineQuickStart5)
* [Quickstart Stage 6 Code](https://github.com/paulWatt526/tileEngineQuickStart6)
* [Quickstart Stage 7 Code](https://github.com/paulWatt526/tileEngineQuickStart7)
* [Quickstart Stage 8 Code](https://github.com/paulWatt526/tileEngineQuickStart8)

Additional Examples

* [Loading level from Tiled](tiledExample.markdown)
* [Integrating Physics Objects](physicsExample.markdown)
* [Using the RegionManager](regionManagerExample.markdown)

### Support

More support is available from the Blind Prophet Software, LLC team:

* [E-mail](mailto:contact@blindprophetsoftware.com)
* [Forum](http://blindprophetsoftware.boards.net)
* [Plugin Publisher](http://www.blindprophetsoftware.com)


## Compatibility

| Platform                     | Supported
| ---------------------------- | ---------------------------- 
| iOS                          | Yes
| Android                      | Yes
| Android (GameStick)          | Yes
| Android (Kindle)             | Yes
| Android (NOOK)               | Yes
| Android (Ouya)               | Yes
| Mac App                      | Yes
| Win32 App                    | Yes
| Windows Phone 8              | Yes
| Corona Simulator (Mac)       | Yes
| Corona Simulator (Win)       | Yes

## Screenshots

### Racing Game

![Racing screenshot 1](img/hgtRacing1.png)

![Racing screenshot 2](img/hgtRacing2.png)

![Racing screenshot 3](img/hgtRacing3.png)

### Roguelike

![Roguelike screenshot 1](img/rogue1.png)

![Roguelike screenshot 2](img/rogue3.png)

![Roguelike screenshot 3](img/rogue4.png)

### Tech Demo

![Tech deom screenshot 1](img/tech1.png)

![Tech deom screenshot 2](img/tech2.png)

![Tech deom screenshot 3](img/tech3.png)

![Tech deom screenshot 4](img/tech4.png)

## Videos

* [Tech Demo](https://youtu.be/eTEtrMImJu0)
* [Racing Example (with parallax)](https://youtu.be/lA7IsWciqCU)

## Release Notes

### 2-24-20

The Wattage Tile Engine is now open source software.

### 7-11-17

Version 1.0.4

This release consists of non-breaking changes.  It adds functions to
RegionManager which allow it to handle non-resource entities.

### 5-8-17

Version 1.0.3

This release consists of non-breaking changes.  No changes should be
necessary in your code.

* Added RegionManager type to assist in creating very large worlds.
* Fixed memory leak occurring when tiles are dynamicaly updated outside
of the visible area.

### 4-25-17

Version 1.0.2

This release consists of non-breaking changes.  No changes should be
necessary in your code.

* Fixed bug where entities in an EntityLayer could be visible on the first
frame before they were moved into correct positions.
* Minor Performance Improvements.
* SpriteInfo.new() has been deprecated.  We have found that calling
new() repeatedly is noticeably more costly than just creating a table
with the same properties.  The new() function has been left in the
engine for now, but it may be removed in the future.  It is recommended
that a table be used instead.  For example, instead of this:

``````lua
local spriteInfo = SpriteInfo.new({
    imageRect = displayObject,
    width = 100,
    height = 100
})
``````

It is slightly better performance wise to do this:

``````lua
local spriteInfo = {
    imageRect = displayObject,
    width = 100,
    height = 100
}
``````

* Introduced lighting mode NONE for layers.  This will skip any light
processing to improve performance for games which just want to display
unlit tiles.

### 2-1-17

Version 1.0.1

This release consists of non-breaking changes.  No changes should be
necessary in your code.

* Fixed bug where tiles may be added twice when scrolling diagonally.
* Fixed bug with non-resource entity ID assignment.  Resource and
non-resource IDs are managed separately.  It is now possible that the same
ID could be assigned to a resource entity as well as a non-resource
entity.