![Wattage Tile Engine Logo](img/logo.png)

# Wattage Tile Engine: Plugin API Docs

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Library](http://docs.coronalabs.com/api/type/Library.html)
| __Corona Store__     | [wattageTileEngine](http://store.coronalabs.com/plugin/wattageTileEngine)
| __Keywords__         | Tiles, Tile, Tile Engine, Engine
| __See also__         | 

## Quickstart

Find screenshots of the tile engine in action [here](#screenshots).

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
* [SpriteInfo](spriteInfo/type_spriteInfo.markdown)
* [Tile](tile/type_tile.markdown)
* [TileLayer](tileLayer/type_tileLayer.markdown)
* [ViewControl](viewControl/type_viewControl.markdown)


## Project Configuration

### Corona Store Activation

In order to use this plugin, you must activate the plugin at the [Corona Store](http://store.coronalabs.com/plugin/wattageTileEngine).


### SDK

When you build using the Corona Simulator, the server automatically takes care of integrating the plugin into your project. 

All you need to do is add an entry into a `plugins` table of your `build.settings`. The following is an example of a minimal `build.settings` file:

``````
settings =
{
	plugins =
	{
		-- key is the name passed to Lua's 'require()'
		["plugin.wattageTileEngine"] =
		{
			-- required
			publisherId = "com.blindprophetsoftware",
		},
	},		
}
``````

### Enterprise

If you have activated this plugin, you can download this plugin from the corresponding plugin page in the [Corona Store](http://store.coronalabs.com/plugin/wattageTileEngine).


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

* [Loading level from Tiled -- Coming VERY soon]()

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

![Racing screenshot 1](img/racing2.png)

![Racing screenshot 1](img/racing3.png)

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