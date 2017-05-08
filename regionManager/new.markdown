# RegionManager.new()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.RegionManager.*](type_regionManager.markdown)
| __Return value__     | [RegionManager](type_regionManager.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function creates a new instance of RegionManager.

## Syntax

	RegionManager.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties. Please reference
the [usage guide](usageGuide.markdown) for more details on these
properties.

##### regionWidthInTiles <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Specifies how many tiles wide each region will be.

##### regionHeightInTiles <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Specifies how many tiles high each region will be.

##### renderRegionWidth <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Specifies how many regions wide the render region will be.

##### renderRegionHeight <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Specifies how many regions high the render region will be.

##### tileSize <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The size of the square tiles.

##### tileLayersByIndex <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
This table needs to contain all the TileLayers keyed by their
layer index.

##### entityLayersByIndex <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
This table needs to contain all the EntityLayers keyed by their
layer index.

##### camera <small>(required)</small>
[Camera](../camera/type_camera.markdown)
Reference to the camera used by the tile engine.

##### listener <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Table containing the following listener functions:

* getRegion(params)
* regionReleased(regionData)

Please reference the [usage guide](usageGuide.markdown) for details
on how to implement these functions.

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local RegionManager = TileEngine.RegionManager

regionManager = RegionManager.new({
    regionWidthInTiles = 3,
    regionHeightInTiles = 3,
    renderRegionWidth = 5,
    renderRegionHeight = 3,
    tileSize = 128,
    tileLayersByIndex = { [1] = bufferLayer },
    entityLayersByIndex = { [2] = entityLayer },
    camera = tileEngineViewControl.getCamera(),
    listener = scene
})
``````
