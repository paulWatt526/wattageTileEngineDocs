# RegionManager

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [RegionManager](type_regionManager.markdown)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Keywords__         | Wattage, RegionManager, Tile Engine
| __See also__         |

## Overview

The RegionManager provides a way to load and unload smaller regions of a
world as they move into and out of the camera's view.  This enables the
Wattage Tile Engine to work with very large worlds which would not fit
into memory if loaded in their entirety.

## Guides

* [Usage Guide](usageGuide.markdown)

## Syntax

	local TileEngine = require "plugin.wattageTileEngine"
	local RegionManagerType = TileEngine.RegionManager

### Constructor

##### [RegionManager.new()](new.markdown)

### Functions

##### [RegionManager.setCameraLocation()](setCameraLocation.markdown)

##### [RegionManager.centerEntityOnTile()](centerEntityOnTile.markdown)

##### [RegionManager.centerNonResourceEntityOnTile()](centerNonResourceEntityOnTile.markdown)

##### [RegionManager.getEntityLocation()](getEntityLocation.markdown)

##### [RegionManager.getNonResourceEntityLocation()](getNonResourceEntityLocation.markdown)

##### [RegionManager.setEntityLocation()](setEntityLocation.markdown)

##### [RegionManager.setNonResourceEntityLocation()](setNonResourceEntityLocation.markdown)